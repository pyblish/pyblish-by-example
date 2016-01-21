### Data

We've briefly touched upon the fact that `Context` and `Instance` objects can store and retrieve `data`.

```python
import pyblish.api
context = pyblish.api.Context()
context.data["key"] = "value"
```

Data is a regular Python dictionary stored in the `Context` and is meant for sharing information amongst plug-ins, whereas data in an `Instance` is specific to the instance. In both cases, data uses `mixedCase` by convention, whereas standard Python variables use `snake_case`.

```python
# wrong
context.data["my_key"] = True

# right
context.data["myKey"] = True
```