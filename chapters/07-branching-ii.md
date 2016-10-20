### Branching II

Let's look at a more interesting branching technique.

```python
import pyblish.api

items = ["john", "door"]

class CollectInstances(pyblish.api.ContextPlugin):
  order = 0

  def process(self, context):
    for item in items:
      context.create_instance(item)

class PrintInstances(pyblish.api.InstancePlugin):
  order = 1

  def process(self, instance):
    print("Instance is: %s" % instance)

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(PrintInstances)

import pyblish.util
pyblish.util.publish()
# The instance is "john"
# The instance is "door"
```

In this case, `PrintInstances` will run once for every instance. That's because we subclassed [InstancePlugin][] instead of [ContextPlugin][].

These two superclasses form the foundation upon which all of Pyblish is built, we'll have a much closer look these at in the following examples.

[ContextPlugin]: https://github.com/pyblish/pyblish.api/wiki/ContextPlugin
[InstancePlugin]: https://github.com/pyblish/pyblish.api/wiki/InstancePlugin
[Context]: https://github.com/pyblish/pyblish.api/wiki/Context
[Instance]: https://github.com/pyblish/pyblish.api/wiki/Instance