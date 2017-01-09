### Architecture

Let's take a moment to talk about the 10.000 feet view of Pyblish.

Besides plug-ins, there are two primary objects that are of interest to you.

1. `Context`
2. `Instance`

The `Context` represents the world, typically your current working file, and contains 1 or more `Instance`.

![image](https://cloud.githubusercontent.com/assets/2152766/12515123/ac0ec266-c11e-11e5-803f-8e83fac3b20d.png)


You can think of `Instance` as a *subdivision* of `Context`, each pertaining to a specific area of the bigger picture, such as an image sequence or a model. When publishing, you can choose to consider either the world or part of the world.

![image](https://cloud.githubusercontent.com/assets/2152766/12515132/b6693872-c11e-11e5-911d-43387571751a.png)

In some cases, it makes sense to only look at a small portion of a working file, either for precision or special treatment. For example, if your `Context` is a scene from Star Wars, you might treat Luke different from how you treat The Death Star.

In other cases, it makes more sense to look at the world as a whole, such as when identifying Luke midst other assets in your scene.

<br>
<br>
<br>

### Cooperation

Now that you're able to write, register and coordinate plug-ins, it's time to look at how to make them cooperate.

```python
import datetime
import pyblish.api

class CollectTime(pyblish.api.ContextPlugin):
  order = 0

  def process(self, context):
    time = datetime.datetime.now()
    context.data["time"] = time

class PrintTime(pyblish.api.ContextPlugin):
  order = 1

  def process(self, context):
    time = context.data["time"]
    print(time)

pyblish.api.register_plugin(CollectTime)
pyblish.api.register_plugin(PrintTime)

import pyblish.util
pyblish.util.publish()
```

You can use this object to pass information from one plug-in to another. The `Context` is also accessible from the return value of `publish()`.

```python
context = pyblish.util.publish()
```
