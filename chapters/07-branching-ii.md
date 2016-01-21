### Branching II

Let's look at a more interesting branching technique.

```python
import pyblish.api

items = ["john", "door"]

class CollectInstances(pyblish.api.ContextPlugin):
  order = 10

  def process(self, context):
    for item in items:
      context.create_instance(item)

class PrintInstances(pyblish.api.InstancePlugin):
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

Pyblish knows to do this because we subclassed from [InstancePlugin][] instead of [ContextPlugin][], which differs in that it runs once for ever available [Instance][] as opposed to just once for the [Context][]. These two superclasses form the foundation upon which all of Pyblish is built, we'll have a much closer look these at in the following examples.