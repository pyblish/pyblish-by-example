### CVEI IV

Sometimes you need more control over ordering, and that's when it can be useful to know that you can *offset* the built-in orders.

```python
import pyblish.api

class PreCollector(pyblish.api.ContextPlugin):
  order = pyblish.api.CollectorOrder - 0.1
  
  def process(self, context):
    context.create_instance("SpecialInstance")
    

class Collector(pyblish.api.ContextPlugin):
  order = pyblish.api.CollectorOrder
  
  def process(self, context):
    special_instance = context["SpecialInstance"]
    special_instance.data["specialData"] = 42
```

You can offset any plug-in from negative 0.499.. to positive 0.499.. A value beyond that will inadvertently transition your plug-in into the next built-in order.

**Ranges**

```yaml
-0.5 to 0.499.. = Collection
0.5 to 1.499.. = Validation
1.5 to 2.499.. = Extraction
2.5 to 3.499.. = Integration
```
