### Quickstart

Before we move on, let me throw you into the deep end and show you a full example.

Don't worry too much if it doesn't make sense just now, the rest of the examples are dedicated to explaining each feature in great detail.

The examples will be written primarily for Autodesk Maya, but should be easily readable and it's concepts applicable to any 3d content creation software. There is a slight simplification involved, for more clarity, but overall this represents a real-world implementation of *a fully featured publishing pipeline with Pyblish*.

### The Deep End

The example uses the 2 available superclasses in Pyblish - `ContextPlugin` and `InstancePlugin`. The order in which these plug-ins are run is controlled by an integer attribute called `order`, with 4 default values.

1. Collection
2. Validation
3. Extraction
4. Integration

![image](https://cloud.githubusercontent.com/assets/2152766/12515092/752725ea-c11e-11e5-923c-ace968721a38.png)

**1. collect_rig.py**

Gather information to validate and export.

```python
import pyblish.api
from maya import cmds

class CollectRig(pyblish.api.ContextPlugin):
  """Discover and collect available rigs into the context"""

  order = pyblish.api.CollectorOrder

  def process(self, context):
    for node in cmds.ls(sets=True):
      if not node.endswith("_RIG"):
        continue
 
      name = node.rsplit("_", 1)[0]
      instance = context.create_instance(name, family="rig")

      # Collect associated nodes
      members = cmds.sets(node, query=True)
      cmds.select([node] + members, noExpand=True)
      instance[:] = cmds.file(
        constructionHistory=True,
        exportSelected=True,
        preview=True,
        force=True)
```

**2. validate_rig.py**

Ensure the correctness of collected information.

```python
import pyblish.api

class ValidateRigContents(pyblish.api.InstancePlugin):
  """Ensure rig has the appropriate object sets"""

  order = pyblish.api.ValidatorOrder
  families = ["rig"]

  def process(self, instance):
    assert "controls_SEL" in instance, "%s is missing a controls set" % instance
    assert "pointcache_SEL" in instance, "%s is missing a pointcache set" % instance
```

**3. extract_rig.py**

Write to disk.

```python
import os
import shutil

import pyblish.api
from maya import cmds

class ExtractRig(pyblish.api.InstancePlugin):
  """Serialise valid rig"""

  order = pyblish.api.ExtractorOrder
  families = ["rig"]
  hosts = ["maya"]

  def process(self, instance):
    context = instance.context
    dirname = os.path.dirname(context.data["currentFile"])
    name, family = instance.data["name"], instance.data["family"]
    date = pyblish.api.format_filename(context.data["date"])

    # Find a temporary directory with support for publishing multiple times.
    tempdir = os.path.join(dirname, "temp", date, family, name)
    tempfile = os.path.join(tempdir, name + ".ma")

    self.log.info("Exporting %s to %s" % (instance, tempfile))

    if not os.path.exists(tempdir):
        os.makedirs(tempdir)

    cmds.select(instance, noExpand=True)  # `instance` a list
    cmds.file(tempfile,
              type="mayaAscii",
              exportSelected=True,
              constructionHistory=False,
              force=True)

    # Store reference for integration
    instance.set_data("tempdir", tempdir)
```

**4. integrate_rig.py**

Integrate written information into the pipeline, as per convention.

```python
import os
import shutil

import pyblish.api

class IntegrateRig(pyblish.api.InstancePlugin):
  """Copy files to an appropriate location where others may reach it"""

  order = pyblish.api.IntegratorOrder
  families = ["rig"]

  def process(self, instance):
    assert instance.data("tempdir"), "Can't find rig on disk, aborting.."

    self.log.info("Computing output directory..")
    context = instance.context
    dirname = os.path.dirname(context.data("currentFile"))
    root = os.path.join(dirname, "public")
    
    if not os.path.exists(root):
        os.makedirs(root)

    version = "v%03d" % (len(os.listdir(root)) + 1)

    src = instance.data("tempdir")
    dst = os.path.join(root, version)

    self.log.info("Copying %s to %s.." % (src, dst))

    shutil.copytree(src, dst)
    self.log.info("Copied successfully!")
```

### That's a lot

I'm sure you have lots of questions, but don't worry. This is the part where we dig into exactly how we get to this point, and what all of this really means.

### Test it out

To run this in your own Maya, copy and run this entire file in your Script Editor.

- [Full Example Source Code](https://gist.github.com/mottosso/93399862c94f0ab4314f)

Open up your Script Editor to inspect its outcome!

### Alternative examples

Looking for a full example for your DCC?

These will turn into links as they become available, watch this space!

- 3ds Max
- Softimage
- Houdini
- Nuke
- Fusion
- Clarisse
- Modo
- Blender