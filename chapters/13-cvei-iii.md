### CVEI III

As a final note - CVEI is a convention for which order to pick for a typical task.

The advantage of using these particular orders isn't as much functional as it is conventional. In fact, the order you assign is just an integer value. 

```python
import pyblish.api

class MyValidator(pyblish.api.ContextPlugin):
  order = pyblish.api.ValidatorOrder  # == 1
```

The benefits of sticking with CVEI are two-fold.

1. The ordering provides a common language with which to discuss publishing.
2. And under the hood, they allow Pyblish to make assumptions about your plug-ins, such as when to abort.

This language fuels our community, and the assumptions are what fuels the mechanics of Pyblish.

With this in mind, saving plug-ins are files are typically named after what they are.

```yaml
plugins
├── collect_my_assets.py
├── validate_normals.py
├── extract_alembic.py
└── integrate_ftrack.py
```
