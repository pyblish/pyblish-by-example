### Branching III

In addition to running a plug-in once for every instance as in the previous example, it can sometimes be useful to define "classes" of instances that a common set of plug-ins can operate on.

Here, a "class of instances" is known as a `family` and a plug-in may support one or more `families`, which is another **requirement attribute**, like `hosts`.

```python
import pyblish.api

items = ["john.person", "door.prop"]

class CollectInstances(pyblish.api.ContextPlugin):
  order = 10

  def process(self, context):
    for item in items:
      name, suffix = item.split(".")
      instance = context.create_instance(name)
      instance.data["families"] = [suffix]

class PrintPersons(pyblish.api.InstancePlugin):
  order = 20
  families = ["person"]

  def process(self, instance):
    print("Person is: %s" % instance)

class PrintProps(pyblish.api.InstancePlugin):
  order = 20
  families = ["prop"]

  def process(self, instance):
    print("The prop is: %s" % instance)

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(PrintPersons)
pyblish.api.register_plugin(PrintProps)

import pyblish.util
pyblish.util.publish()
# The person is "john"
# The prop is "door"
```

If you pay special attention to the final output, you can see that "john" was processed by `PrintPersons`, whereas "door" got processed by `PrintProps`.
