# Callback II

You can emit and catch your own signals.

```python
import pyblish.api

class MyCollector(pyblish.api.ContextPlugin):
    order = pyblish.api.CollectorOrder

    def process(self, context):
        pyblish.api.emit("myEvent", data="myData")
```

You can then catch this signal anywhere in your program.

```python
import pyblish.api

def on_my_event(data):
  print(data)
 
pyblish.api.register_callback("myEvent", on_my_event)
```

Callbacks can be useful for, amongst other things:

- Deep customisation
- Advanced logging
- Tighter integration
 
On a technical note, callbacks are run on the main thread and block until finished. This means that if for example one of your callbacks would take 10 seconds to finish, publishing overall will take 10 seconds longer. On the upside, it also means that the Context will accurately reflect the current state at the time of a signal emitting.