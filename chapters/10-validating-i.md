### Validating I

Sometimes, sharing means to first agree on a format in which to share, such that you don't end up with one big mess.

```python
import pyblish.api

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

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(ValidateNamingConvention)

import pyblish.util
pyblish.util.publish()
# Sorry, JOHN should have been John
# Sorry, door should have been Door
Stopped due to: failed validation
```

We indicate failure by throwing exceptions of any kind, including assertions. Making the change, we now "pass validation".

```python
...
items = ["John.person", "Door.prop"]
...
pyblish.util.publish()
# John is valid
# Door is valid
```