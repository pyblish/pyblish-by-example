### Sharing

Publishing is about sharing, so let's have a look at how to publish something other than by printing.

```python
import os
import datetime
import pyblish.api

class CollectUserDir(pyblish.api.ContextPlugin):
  order = 10

  def process(self, context):
    context.data["userDir"] = os.path.expanduser("~")

class WriteTime(pyblish.api.ContextPlugin):
  order = 20

  def process(self, context):
    user_dir = context.data["userDir"]
    destination_path = os.path.join(user_dir, "time.txt")

    print("Writing time to %s" % destination_path)
    with open(destination_path, "w") as f:
      f.write("The time is %s" % datetime.datetime.today().ctime())

pyblish.api.register_plugin(CollectUserDir)
pyblish.api.register_plugin(WriteTime)

import pyblish.util
pyblish.util.publish()
# Writing time to C:\Users\marcus\Documents\time.txt
```

And here's what `time.txt` looks like.

```bash
The time is Thu Jan 21 16:34:58 2016
```