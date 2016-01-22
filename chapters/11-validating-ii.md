### Validating II

In the previous example, we ensured that instances are title-cased. But failure doesn't stop subsequent plug-ins from actually writing to disk.

```python
import pyblish.api

disk = {}
items = ["JOHN.person", "door.prop"]

class CollectInstances(pyblish.api.Plugin):
  order = 10

  def process(self, context):
    for item in items:
      name, suffix = item.split(".")
      context.create_instance(name, family=suffix)

class ValidateNamingConvention(pyblish.api.Plugin):
  order = 20

  def process(self, instance):
    name = instance.data["name"]
    assert name == name.title(), "Sorry, %s should have been %s" % (
      name, name.title())

class ExtractInstances(pyblish.api.Plugin):
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

To remedy this, we can write a "test" that looks like this.

```python
def my_test(**vars):
  if vars["nextOrder"] >= 30 and 20 in vars["ordersWithError"]:
    return "failed validation, sorry!"

pyblish.api.register_test(my_test)
```

The test can be visualised graphically like this.

![image](https://cloud.githubusercontent.com/assets/2152766/12515092/752725ea-c11e-11e5-923c-ace968721a38.png)

The reason for its complexity comes from the fact that we wish *all* validators to run before stopping, even if the first one fails, such that we can get a complete overview of what went wrong.

Don't worry, you won't actually have to write or understand how tests work. The default test provided by Pyblish covers the majority of use-cases, and we'll take a closer look at this in the next example.

For now, all you need to know is that it exists and is customisable should you need it.

Here is the full source code, if you would like to try it out.

```python
import pyblish.api

disk = {}
items = ["JOHN.person", "door.prop"]

class CollectInstances(pyblish.api.Plugin):
  order = 10

  def process(self, context):
    for item in items:
      name, suffix = item.split(".")
      context.create_instance(name, family=suffix)

class ValidateNamingConvention(pyblish.api.Plugin):
  order = 20

  def process(self, instance):
    name = instance.data["name"]
    assert name == name.title(), "Sorry, %s should have been %s" % (
      name, name.title())

class ExtractInstances(pyblish.api.Plugin):
  order = 30

  def process(self, instance):
    disk[instance.data["name"]] = instance


def my_test(**vars):
  if vars["nextOrder"] >= 30 and 20 in vars["ordersWithError"]:
    return "failed validation, sorry!"

pyblish.api.register_plugin(CollectInstances)
pyblish.api.register_plugin(ValidateNamingConvention)
pyblish.api.register_plugin(ExtractInstances)
pyblish.api.register_test(my_test)

import pyblish.util
pyblish.util.publish()
# Publishing stopped due to failed validation, sorry!
print("JOHN" in disk)
# False
```