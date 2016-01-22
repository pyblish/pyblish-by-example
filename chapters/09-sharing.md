### Sharing

Publishing is about sharing, so let's have a look at how to publish something other than by printing.

```python
import os
import pyblish.api

class CollectUserDir(pyblish.api.Plugin):
  order = 10

  def process(self, context):
    context.data["userDir"] = os.path.expanduser("~")

class WriteTime(pyblish.api.Plugin):
  order = 20

  def process(self, context, time):
    user_dir = context.data["userDir"]
    destination_path = os.path.join(user_dir, "time.txt")

    with open(destination_path, "w") as f:
      f.write("The time is %s" % time())

pyblish.api.register_plugin(CollectUserDir)
pyblish.api.register_plugin(WriteTime)

import pyblish.util
pyblish.util.publish()
# Writing time to C:\Users\marcus\Documents\time.txt
```

And here's what `time.txt` looks like.

```bash
The time is 2015-06-10T10:38:04.426000Z
```