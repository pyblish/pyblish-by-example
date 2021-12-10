### Filtering

Filtering is handy when more control over your plugins is needed. 

<br>
After registering a callback function, it'll run on all registered plugins during discovery.
This is usefull to overwrite the settings of registered plugins.

<br>
<br>
Example: we overwrite a hardcoded export path so we can reuse this plugin for our new project, without having to write and register a new plugin.

<br>
<br>

```python
import pyblish.api

class MyExportPlugin(pyblish.api.ContextPlugin):
  export_path = 'C:/project_alpha/models'
  def process(self, context):
    print('export to:' + self.export_path)

pyblish.api.register_plugin(MyExportPlugin)

def export_path_filter(plugins):
  for plugin in plugins:
    if hasattr(plugin, 'export_path'):
      plugin.export_path = 'D:/project_beta/models'

pyblish.api.register_discovery_filter(export_path_filter)

import pyblish.util
pyblish.util.publish()
#export to:D:/project_beta/models
```


You can register a filter using `api.register_discovery_filter.`

Note that functions stay registered and wont update when you re-register them with the same name. You have to either deregister the original one, or use 
`pyblish.api.deregister_all_discovery_filters()` to unregister all filters.
