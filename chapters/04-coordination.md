### Coordination

In the previous example, you might have gotten the reverse output.

```bash
# hello from plugin2
# hello from plugin1
```

That's because plug-ins are sorted by the class attribute `order`, and we didn't change it.

```python
import pyblish.api

class FirstPlugin(pyblish.api.Plugin):
  order = 10

  def process(self):
    print("hello")

class SecondPlugin(pyblish.api.Plugin):
  order = 20

  def process(self):
    print("world")

pyblish.api.register_plugin(FirstPlugin)
pyblish.api.register_plugin(SecondPlugin)

import pyblish.util
pyblish.util.publish()
# hello
# world
```

They now run in the expected order.