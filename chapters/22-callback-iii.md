# Callback III

As a final, practical example of callbacks, consider the following.

```python
import pyblish.api
from maya import cmds

def on_instance_toggled(instance, new_value, old_value):
  node = instance.data["nodeName"]
  cmds.setAttr(node + ".publish", new_value)
```

Assuming that the publishable state of your instance in Maya is determined by the user-defined attribute "publish", this callback will cause the GUI to persist the toggled state of any given instance directly in your scene.

Now, both when you reset Pyblish, reload your scene or even save the file and restart Maya, the state at which it was visually toggled will persist.

