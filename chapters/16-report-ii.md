### Report II

In addition to visualising which plug-in processed which instance, it would also be helpful to visualise error messages (if any). So that's what we'll do in this example.

```python
Success   Plug-in                                   -> Instance
----------------------------------------------------------------------
1         CollectCaptainAmerica                     -> None
0         ValidateCaptainAmerica                    -> Captain America
          +-- EXCEPTION: Captain America must be a hero
```

Building from our previous example, this is how to format it in order to end up with the above.

```python
header = "{:<10}{:<40} -> {}".format("Success", "Plug-in", "Instance")
result = "{success:<10}{plugin.__name__:<40} -> {instance}"
error = "{:<10}+-- EXCEPTION: {:<70}"

results = list()
for r in context.data["results"]:
  results.append(result.format(**r))
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

Now all error messages are neatly printed in a tree-like fashion underneath each relevant result.