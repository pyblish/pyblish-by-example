### CVEI II

Sometimes the file-management part of extraction is better kept separate.

In this example, we will:

1. Simulate an Autodesk Maya environment
2. Extract some data from it
3. Integrate this data with a server
4. Without making reference to the simulated environment

Our environment.

```python
import sys

disk = {}
server = {}

class cmds:
  @staticmethod
  def ls(type, assemblies):
    return maya.scene.keys()

  @staticmethod
  def file(path, exportSelected):
    disk[path] = maya.scene[maya.selected]

  @staticmethod
  def select(node):
    maya.selected = node

class maya:
  selected = None
  cmds = cmds
  scene = {
    "john": 0xb3513451, # Binary
    "door": 0x516b481f,
  }

sys.modules["maya"] = maya
```

We can now `from maya import cmds`, which we will use during collection and extraction.

```python
import pyblish.api
from maya import cmds

class CollectInstances(pyblish.api.ContextPlugin):
  order = pyblish.api.CollectorOrder

  def process(self, context):
    for name in cmds.ls(type="transform", assemblies=True):
      context.create_instance(name)

class ExtractInstances(pyblish.api.InstancePlugin):
  order = pyblish.api.ExtractorOrder

  def process(self, instance):
    # 1. Compute temporary output path
    name = instance.data["name"]
    transient_path = "c:\temp\%s.mb" % name

    # 2. Perform serialisation
    cmds.select(name)
    cmds.file(transient_path, exportSelected=True)

    # 3. Store reference for subsequent plug-ins
    instance.data["transientDest"] = transient_path
```

Now let's integrate the data from `temp` on `disk` into our `server`.

```python
class IntegrateInstances(pyblish.api.InstancePlugin):

  order = pyblish.api.IntegratorOrder

  def process(self, instance):
    transient_dest = instance.data["transientDest"]
    permanent_dest = "/instances/%s.mb" % instance
    server[permanent_dest] = disk[transient_dest]
```

Putting it all together, this is the full source code.

```python
import sys

disk = {}
server = {}

class cmds:
  @staticmethod
  def ls(type, assemblies):
    return maya.scene.keys()

  @staticmethod
  def file(path, exportSelected):
    disk[path] = maya.scene[maya.selected]

  @staticmethod
  def select(node):
    maya.selected = node

class maya:
  selected = None
  cmds = cmds
  scene = {
    "john": 0xb3513451, # Binary
    "door": 0x516b481f,
  }

sys.modules["maya"] = maya

import pyblish.api
from maya import cmds

class CollectInstances(pyblish.api.ContextPlugin):
  order = pyblish.api.CollectorOrder

  def process(self, context):
    for name in cmds.ls(type="transform", assemblies=True):
      context.create_instance(name)

class ExtractInstances(pyblish.api.InstancePlugin):
  order = pyblish.api.ExtractorOrder

  def process(self, instance):
    # 1. Compute temporary output path
    name = instance.data["name"]
    transient_path = "c:\temp\%s.mb" % name

    # 2. Perform serialisation
    cmds.select(name)
    cmds.file(transient_path, exportSelected=True)

    # 3. Store reference for subsequent plug-ins
    instance.data["transientDest"] = transient_path

class IntegrateInstances(pyblish.api.InstancePlugin):
  order = pyblish.api.IntegratorOrder

  def process(self, instance):
    transient_dest = instance.data["transientDest"]
    permanent_dest = "/instances/%s.mb" % instance
    server[permanent_dest] = disk[transient_dest]


pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(ExtractInstances)
pyblish.api.register_plugin(IntegrateInstances)

import pyblish.util
pyblish.util.publish()
print disk
print server
# {'c:\temp\\john.mb': 3008443473L, 'c:\temp\\door.mb': 1365985311}
# {'/instances/john.mb': 3008443473L, '/instances/door.mb': 1365985311}
```

The key point to take away from this example is that file-management is independent of serialisation.