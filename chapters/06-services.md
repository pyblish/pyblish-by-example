### Services

The special argument `context` from above is provided via a feature of the run-time called Dependency Injection. In a nutshell, it means that things you require are provided to you, given that you ask for it. In this case, we asked to gain access to the `context`, and so the `context` was provided to us.

The objects provided are called services and this is how you can provide your own.

```python
import pyblish.api

class MyPlugin(pyblish.api.Plugin):
  def process(self, myvalue):
    print("Value is: %i" % myvalue)

pyblish.api.register_plugin(MyPlugin)
pyblish.api.register_service("myvalue", 5)

import pyblish.util
pyblish.util.publish()
# Value is 5
```

Services can be any Python object, including callables. Callables are well suited for values that aren't static, such as time.

```python
import datetime
import pyblish.api

class MyPlugin(pyblish.api.Plugin):
  def process(self, time):
    print("The current time is: %s" % time())

pyblish.api.register_plugin(MyPlugin)
pyblish.api.register_service("time", datetime.datetime.now)

import pyblish.util
pyblish.util.publish()
# The current time is 2015-06-09 12:32:10.283000
```

As it happens, a few services are provided by default, including `time`.

- `user` is available by value, as it is not expected to change at run-time.
- `time` is callable, as it provides unique values each time it is used
- `config` is shorthand to `pyblish.api.config`

Along with one more special service, called `instance` which we will look at next.