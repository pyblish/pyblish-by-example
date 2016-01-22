### Files

Plug-ins can also be stored as files.
```bash
myplugins
├── myplugin1.py
└── myplugin2.py
```

Here is the full source code.

```python
# myplugin1.py
import pyblish.api

class MyPlugin1(pyblish.api.Plugin):
  def process(self):
    print("hello from plugin1")
```

```python
# myplugin2.py
import pyblish.api

class MyPlugin2(pyblish.api.Plugin):
  def process(self):
    print("hello from plugin2")
```

You then register their parent directory, similar to how you would normally register Python modules.

```bash
# Environment Variables: Windows
$ set PYBLISHPLUGINPATH=c:\myplugins;\\server\moreplugins

# Environment Variables: Unix
$ export PYBLISHPLUGINPATH=/myplugins:/moreplugins
```

You can also register from Python.

```python
import pyblish.api
pyblish.api.register_plugin_path(r"c:\myplugins")
```

Once registered, the plug-ins are triggered upon the next publish.

```python
import pyblish.util
pyblish.util.publish()
# hello from plugin1
# hello from plugin2
```

**See also**

- [Task-based plug-in registration](http://forums.pyblish.com/t/task-specific-plugins)