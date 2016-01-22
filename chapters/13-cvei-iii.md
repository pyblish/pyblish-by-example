### CVEI III

As a final note about CVEI, it's a convention on which order to pick for a typical task.

The advantage of using these particular orders isn't as much functional as it is conventional. The benefits are two-fold.

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
