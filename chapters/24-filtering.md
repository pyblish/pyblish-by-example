### Filtering

Filtering is handy when more control over your plugins is needed. 

After registering a callback function, it'll run on all registered plugins during discovery. This is useful to overwrite the settings of registered plugins.

For example, here's how we can overwrite a hardcoded export path so as to reuse a plugin for another project, without having to write and register a new plugin.

```python
import pyblish.api

# The original plug-in
class MyExportPlugin(pyblish.api.ContextPlugin):
  export_path = "C:/project_alpha/models"
  def process(self, context):
    print("Exported to: '%s'" % self.export_path)

pyblish.api.register_plugin(MyExportPlugin)

# Our custom "filter"
def export_path_filter(plugins):
  for plugin in plugins:
    if hasattr(plugin, 'export_path'):
      plugin.export_path = 'D:/project_beta/models'

pyblish.api.register_discovery_filter(export_path_filter)

import pyblish.util
pyblish.util.publish()
# Exported to 'to:D:/project_beta/models'
```

You can register a filter using `api.register_discovery_filter.`

Note that functions stay registered and won't update when you re-register them with the same name. You have to either deregister the original one, or use 
`pyblish.api.deregister_all_discovery_filters()` to unregister all filters.
