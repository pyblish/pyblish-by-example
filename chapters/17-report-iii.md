### Report III

Exception messages are useful, but what would make it even more useful is progress messages. Something that can tell us more about the *why* of an exception.

Progress messages are made using the standard Python logging mechanism.

Here is what we will be developing in this example.

```bash
1         CollectCaptainAmerica                     -> None
0         ValidateCaptainAmerica                    -> Captain America
          +-- INFO: Entering validator..
          +-- INFO: About to validate instance: "Captain America"
          +-- WARNING: Something is not right, aborting..
          +-- EXCEPTION: Captain America must be a hero
```

For this, we will utilise the built-in logger.

```python
class ValidateCaptainAmerica(pyblish.api.InstancePlugin):
  order = pyblish.api.ValidatorOrder

  def process(self, instance):
    self.log.info("Entering validator..")
    self.log.info("About to validate instance: %s" % instance)

    if not instance.data["isHero"]:
        self.log.warning("Something is not right.. aborting")
        raise Exception("%s must be a hero" % instance)
```

Now it's time to format the results.

```python
header = "{:<10}{:<40} -> {}".format("Success", "Plug-in", "Instance")
result = "{success:<10}{plugin.__name__:<40} -> {instance}"
error = "{:<10}+-- EXCEPTION: {:<70}"
record = "{:<10}+-- {level}: {message:<70}"

results = list()
for r in context.data["results"]:
  # Format summary
  results.append(result.format(**r))

  # Format log records
  for lr in r["records"]:
    results.append(record.format("", level=lr.levelname, message=lr.message))

  # Format exception (if any)
  if r["error"]:
    results.append(error.format("", r["error"]))

report = """
{header}
{line}
{results}
"""
print(report.format(header=header,
                    results="\n".join(results),
                    line="-" * 70))
```

Putting it all together, here is the full source code.

```python
import pyblish.api

class CollectCaptainAmerica(pyblish.api.ContextPlugin):
  order = pyblish.api.CollectorOrder

  def process(self, context):
    context.create_instance("Captain America", isHero=False)

class ValidateCaptainAmerica(pyblish.api.InstancePlugin):
  order = pyblish.api.ValidatorOrder

  def process(self, instance):
    self.log.info("Entering validator..")
    self.log.info("About to validate instance: %s" % instance)

    if not instance.data.get("isHero"):
        self.log.warning("Something is not right.. aborting")
        raise Exception("%s must be a hero" % instance)

pyblish.api.register_plugin(CollectCaptainAmerica)
pyblish.api.register_plugin(ValidateCaptainAmerica)

import pyblish.util
context = pyblish.util.publish()

header = "{:<10}{:<40} -> {}".format("Success", "Plug-in", "Instance")
result = "{success:<10}{plugin.__name__:<40} -> {instance}"
error = "{:<10}+-- EXCEPTION: {:<70}"
record = "{:<10}+-- {level}: {message:<70}"

results = list()
for r in context.data["results"]:
  # Format summary
  results.append(result.format(**r))

  # Format log records
  for lr in r["records"]:
    results.append(record.format("", level=lr.levelname, message=lr.message))

  # Format exception (if any)
  if r["error"]:
    results.append(error.format("", r["error"]))

report = """
{header}
{line}
{results}
"""
print(report.format(header=header,
                    results="\n".join(results),
                    line="-" * 70))
```