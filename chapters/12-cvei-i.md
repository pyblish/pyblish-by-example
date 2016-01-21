### CVEI I

Because the order of the above technique of (1) collecting, (2) validating and (3) extract-if-valid is so common, they are provided as keywords you can use in-place of a hard-coded number.

```python
import pyblish.api

disk = {}
items = ["JOHN.person", "door.prop"]

class CollectInstances(pyblish.api.ContextPlugin):

  order = pyblish.api.CollectorOrder  # <-- This is new

  def process(self, context):
    for item in items:
      name, suffix = item.split(".")
      context.create_instance(name, family=suffix)

class ValidateNamingConvention(pyblish.api.InstancePlugin):

  order = pyblish.api.ValidatorOrder

  def process(self, instance):
    name = instance.data["name"]
    assert name == name.title(), "Sorry, %s should have been %s" % (
      name, name.title())

class ExtractInstances(pyblish.api.InstancePlugin):

  order = pyblish.api.ExtractorOrder

  def process(self, instance):
    disk[instance.data["name"]] = instance

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(ValidateNamingConvention)
pyblish.api.register_plugin(ExtractInstances)

import pyblish.util
pyblish.util.publish()
# Sorry, JOHN should have been John
# Sorry, door should have been Door
```

Notice that instead of picking a number at random, we instead utilised the built-in order of CVEI. This not only simplifies determining the role of each plug-in, it also allows Pyblish to make some basic assumptions about your plug-ins, such as when to stop.

These *constants* are nothing more than integer numbers.

```yaml
CollectorOrder: 0
ValidatorOrder: 1
ExtractorOrder: 2
```

Together, they form the first three letters of "CVEI". We'll look at the last letter next.