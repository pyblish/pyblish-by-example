# Callback

Sometimes you may be interested in an event taking place at a particular location during processing.

```python
import pyblish.api

def on_publish(context):
  has_error = any(result["error"] is not None for result in context.data["results"])
  print("Publishing %s" % "finished" if has_error else "failed")
 
pyblish.api.register_callback("event", on_event)
```

This will cause "Publishing finished" or "Publishing failed" to be printed upon completed publishing, based on whether it completed successfully or not.
