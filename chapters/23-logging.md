### Logging

Pyblish does not produce any output unless you explicitly tell it to.

If you enable the `DEBUG` level whilst developing plug-ins, Pyblish can tell you a few things about what is going on.

```python
import logging
import pyblish.api

# Step 0, this doesn't produce any warnings..
pyblish.api.discover()

# Step 1, bring out the debug level messages
logging.getLogger("pyblish").setLevel(logging.DEBUG)

# Step 2, unless there already is a handler, one must be setup.
logging.basicConfig()

# Step 3, done
pyblish.api.discover()
# DEBUG:pyblish.plugin:Skipped: "collect_myplugin" (name 'pybddlish' is not defined)
```

The handler can be customised to tailor the format and contents of the messages, like a timestamp and what not.