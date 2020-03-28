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

Read up on standard Python logging and corresponding handlers for more details.

<br>

### Formatting

In the above example, messages weren't very pretty. You can control the formatting of messages like this.

```py
# Fetch the logger Pyblish uses for all of its messages
log = logging.getLogger("pyblish")

# Do what `basicConfig` does, except explicitly
# and with control over where and how messages go
hnd = logging.StreamHandler()
fmt = logging.Formatter('%(message)s')
hnd.setFormatter(fmt)
log.addHandler(hnd)

pyblish.api.discover()
# Skipped: "collect_myplugin" (name 'pybddlish' is not defined)
```

That `%(message)s` is one of the many variables available during formatting, see here for a full list.

- https://docs.python.org/2/library/logging.html#logrecord-attributes

<br>

### Gotchas

- `basicConfig` will register a handler too, and it's possible to have many. See `log.handlers` for the ones currently registered, it's a plain Python `list` that you can clear to get rid of them.
- Autodesk Maya is special, it runs the equivalent of `basicConfig` under-the-hood at startup. Which means that you always see these messages whether you want to or not. You can remove handlers, and edit them despite this.
- Standalone Python doesn't have any handlers registered, and needs something like the above.
- See or start a conversation about this [on the forums](https://forums.pyblish.com/t/error-handling-on-plugins/596/3)
