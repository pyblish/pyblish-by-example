### Callback I

Sometimes you may be interested in an event taking place at a particular location during processing.

```python
import pyblish.api

def on_published(context):
  has_error = any(result["error"] is not None for result in context.data["results"])
  print("Publishing %s" % ("finished" if has_error else "failed"))

pyblish.api.register_callback("published", on_published)
```

This will cause `"Publishing finished"` or `"Publishing failed"` to be printed upon completed publishing, based on whether it completed successfully or not.

The arguments provided by the signal must match those in your callback. See [here][events] for a complete list of signals emitted in Pyblish.

- [Events][events]

[events]: https://pyblish.gitbooks.io/api/content/pages/Events.html