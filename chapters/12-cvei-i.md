### CVEI I

Because the above technique of (1) collecting, (2) validating and (3) extract-if-valid is so common, they are each provided as a superclass.

```python
import pyblish.api

disk = {}
items = ["JOHN.person", "door.prop"]

class CollectInstances(pyblish.api.Collector):
  def process(self, context):
    for item in items:
      name, suffix = item.split(".")
      context.create_instance(name, family=suffix)

class ValidateNamingConvention(pyblish.api.Validator):
  def process(self, instance):
    name = instance.data["name"]
    assert name == name.title(), "Sorry, %s should have been %s" % (
      name, name.title())

class ExtractInstances(pyblish.api.Extractor):
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

Notice that we didn't have to specify an `order` nor create and register a test. Each variation comes with a pre-determined order. The default test then take it into consideration.

```yaml
Collector: 0
Validator: 1
Extractor: 2
```

Together, they form the first three letters of "CVEI". We'll look at the last letter next.