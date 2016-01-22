### Branching II

Let's look at a more interesting branching technique.

```python
import pyblish.api

items = ["john", "door"]

class CollectInstances(pyblish.api.Plugin):
  order = 10

  def process(self, context):
    for item in items:
      context.create_instance(item)

class PrintInstances(pyblish.api.Plugin):
  order = 20

  def process(self, instance):
    print("Instance is: %s" % instance)

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(PrintInstances)

import pyblish.util
pyblish.util.publish()
# The instance is "john"
# The instance is "door"
```

In this case, `PrintInstances` will run once for every instance.

Pyblish knows to do this because it asks specifically for `instance`, if it didn't it would only be processed a single time. This is a very powerful technique, one we'll have a much closer look at in the following examples.