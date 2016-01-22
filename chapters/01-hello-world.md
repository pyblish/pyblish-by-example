### Hello World

Our first publish will be about printing the classic "Hello World" to the screen. Here is the full source code.

```python
import pyblish.api

class MyPlugin(pyblish.api.Plugin):
  def process(self):
    print("hello python")

pyblish.api.register_plugin(MyPlugin)

import pyblish.util
pyblish.util.publish()
```

Running this in any Python environment, such as a standalone or built-in interpreter, will cause `hello python` to be printed to the screen.