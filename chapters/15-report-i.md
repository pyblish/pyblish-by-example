### Report I

Publishing is about finding problems and the only way to find them is by bringing them to the surface, to visualise them. So in this example, we'll have a look at how you can do just that.

We can use the results produced during publishing to pretty-print ourselves a report of how things went. This is what we will be producing in this example.

```bash
Success   Plug-in                                   -> Instance
----------------------------------------------------------------------
1         CollectCaptainAmerica                     -> None
0         ValidateCaptainAmerica                    -> Captain America
```

Let's dive into the plug-ins now.

```python
import pyblish.api

class CollectCaptainAmerica(pyblish.api.Collector):
  def process(self, context):
    context.create_instance("Captain America", isHero=False)

class ValidateCaptainAmerica(pyblish.api.Validator):
  def process(self, instance):
    # Any raised exception will mark a plug-in as failed
    assert instance.data.get("isHero") == True, "%s must be a hero" % instance

pyblish.api.register_plugin(CollectCaptainAmerica)
pyblish.api.register_plugin(ValidateCaptainAmerica)

import pyblish.util
context = pyblish.util.publish()
```

With `context` at hand, we can now format the results using the `results` dictionary stored within.

```python
results = context.data.get("results")
header = "{:<10}{:<40} -> {}".format("Success", "Plug-in", "Instance")
result = "{success:<10}{plugin.__name__:<40} -> {instance}"
results = "\n".join(template.format(**r) for r in results)
report = """
{header}
{line}
{results}
"""
print(report.format(header=header,
                    results=results,
                    line="-" * 70))
```

The actual output is this.

```bash
Success   Plug-in                                   -> Instance
----------------------------------------------------------------------
1         CollectCurrentWorkingDirectory            -> None
1         CollectCaptainAmerica                     -> None
1         CollectCurrentUser                        -> None
0         ValidateCaptainAmerica                    -> Captain America
```

The plug-ins `CollectCurrentWorkingDirectory` and `CollectCurrentUser` are included by default with Pyblish and adds the following data to the context.

```yaml
cwd: The current working directory at the time of publish
user: The currently logged on user
```