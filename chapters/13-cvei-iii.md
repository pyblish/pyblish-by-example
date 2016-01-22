### CVEI III

As a final note about CVEI, here is their full source code, excluding docstrings.

```python
class Collector(pyblish.api.Plugin):
  order = 0

class Validator(pyblish.api.Plugin):
  order = 1

class Extractor(pyblish.api.Plugin):
  order = 2

class Integrator(pyblish.api.Plugin):
  order = 3
```

The advantage of using these subclasses clearly isn't functional, but conventional. The benefits are two-fold.

1. They provide a common language with which to discuss publishing.
2. They allow Pyblish to make assumptions about your plug-ins, such as when to abort.

The language is what fuels the community, whereas the assumptions are what fuels the mechanics of Pyblish and it's graphical user interfaces.

On a final note, when saving CVEI plug-ins as files, it is also conventional to prefix your file with their verb.

```yaml
plugins
├── collect_instances.py
├── validate_instances.py
├── extract_instances.py
└── integrate_instances.py
```

> Collections is a.k.a. Selection and Integration is a.k.a. Conform