### Architecture

Let's take a moment to talk about the 10.000 feet view of Pyblish.

Besides plug-ins, there are two primary objects that are of interest to you.

1. `Context`
2. `Instance`

The `Context` represents the world, typically your current working file, and contains 1 or more `Instance`.

<img src="/uploads/default/original/1X/8c3cd97a282a0f7991caea588f3629dfb27988e1.png" width="241" height="185">

You can think of `Instance` as a *subdivision* of `Context`, each pertaining to a specific area of the bigger picture, such as an image sequence or a model. When publishing, you can choose to consider either the world, part of the world, or both.

<img src="/uploads/default/original/1X/226e0570eb17098b01b9312ccb985f47d8de3879.png" width="243" height="179"> 

In some cases, it makes sense to only look at a small portion of a working file, either for precision or special treatment. If your `Context` is a scene from Start Wars, you might treat Luke different from how you treat The Death Star, for example.

In other cases, it makes more sense to look at the world as a whole, such as when identifying Luke amidst other assets in your scene.

<br>
<br>
<br>

### Cooperation

Now that you're able to write, register and coordinate plug-ins, it's time to look at how to make them cooperate.

```python
import datetime
import pyblish.api

class CollectTime(pyblish.api.Plugin):
  order = 10

  def process(self, context):
    time = datetime.datetime.now()
    context.data["time"] = time

class PrintTime(pyblish.api.Plugin):
  order = 20

  def process(self, context):
    time = context.data["time"]
    print(time)

pyblish.api.register_plugin(CollectTime)
pyblish.api.register_plugin(PrintTime)

import pyblish.util
pyblish.util.publish()
```

`context` is a special argument in Pyblish. By adding this to the list of arguments to `process()`, you gain access to an the current `Context`, as mentioned above.

This object is shared amongst plug-ins and can be used to pass information from one plug-in to another. The `Context` is also accessible from the return value of `publish()`.

```python
context = pyblish.util.publish()
```