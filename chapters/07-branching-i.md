### Branching I

Now that you know how to arrange plug-ins, let's have a look at how to manage the control flow of publishing.

```python
import pyblish.api

class MyPlugin(pyblish.api.Plugin):
  hosts = ["maya"]

  def process(self):
    from maya import cmds
    cmds.headsUpMessage("Hello from Pyblish")

pyblish.api.register_plugin(MyPlugin)

import pyblish.util
pyblish.util.publish()
# Hello from Pyblish
```

`hosts` is a **requirement attribute** and limits plug-ins to a particular scenario.

In this case, the plug-in will only run when publishing from within Autodesk Maya. These are some examples of available values for the `hosts` attribute.

- `python`
- `maya`
- `houdini`
- `nuke`
- `modo`
- `unknown`

You can register your own host, if for example you would like to extend Pyblish for use in additional software, by using `register_host()`.

```python
import pyblish.api
pyblish.api.register_host("myhost")
```