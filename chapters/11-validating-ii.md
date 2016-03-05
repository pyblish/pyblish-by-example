### Validating II

In the previous example, we ensured that instances are title-cased. But failure doesn't stop subsequent plug-ins from actually writing to disk.

```python
import pyblish.api

disk = {}
items = ["JOHN.person", "door.prop"]

class CollectInstances(pyblish.api.ContextPlugin):
  order = 10

  def process(self, context):
    for item in items:
      name, suffix = item.split(".")
      context.create_instance(name, family=suffix)

class ValidateNamingConvention(pyblish.api.InstancePlugin):
  order = 20

  def process(self, instance):
    name = instance.data["name"]
    assert name == name.title(), "Sorry, %s should have been %s" % (
      name, name.title())

class ExtractInstances(pyblish.api.InstancePlugin):
  order = 30

  def process(self, instance):
    disk[instance.data["name"]] = instance

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(ValidateNamingConvention)
pyblish.api.register_plugin(ExtractInstances)

import pyblish.util
pyblish.util.publish()
print("JOHN" in disk)
# True
```

To remedy this, we'll turn our attention to some of the pre-defined *orders* provided by Pyblish.

- Collection
- Validation
- Extraction
- Integration

Collection sets the stage for validation. Once validation is complete, Pyblish takes a moment to consider whether any of the plug-ins that ran threw an error. If it did, it stops processing and returns control to the user. 

This behavior is paramount to publishing. If you think back to [Quickstart](Quickstart.md) earlies in this guide, you may remember the following visualisation of it.

![image](https://cloud.githubusercontent.com/assets/2152766/12515092/752725ea-c11e-11e5-923c-ace968721a38.png)

In the next example, we will dig deeper into this mechanism and find out more about what it can do for us.
