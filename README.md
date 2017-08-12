![Pyblish by Example](https://cloud.githubusercontent.com/assets/2152766/12489260/51843d38-c067-11e5-93c8-7b96c30ed37a.png)

Welcome to the Pyblish by Example tutorial.

<br>
<br>
<br>

### You will learn

- The basics of publishing in the production of film and games
- The fundamentals of [Pyblish][] and it's [API][]
- How to validate content
- How to guarantee valid content on export 
- How to properly position and name content according to convention
- How to visualise the results of one or more publishes
- Developer and Artist communication through the UI

[Pyblish]: http://pyblish.com
[API]: http://api.pyblish.com

<br>
<br>
<br>

### Introduction

Pyblish is an open source, cross-platform framework for test-driven content creation.

*Pyblish by Example* is a hands-on introduction to Pyblish using short example programs written like a book - to be read from top to bottom.

- [What is Publishing?](https://github.com/pyblish/pyblish/wiki/What-is-publishing)

<br>
<br>
<br>

### Installation

If you haven't already, go ahead and install Pyblish.

```bash
$ pip install pyblish-base
```

Any problems, have a look at the [extended installation guide](http://forums.pyblish.com/t/pyblish-1-4-released/239/2).

<br>
<br>
<br>

### How to use this guide

Start by confirming to yourself that you are indeed using version 1.4+ of Pyblish.

```python
>>> import pyblish
>>> pyblish.__version__
'1.4.3'
```

If not, see the top-left corner of this page for a dropdown of your version.

As you read through this guide it is recommended that you use the scripting API, accessible via `pyblish.util`.

```python
from pyblish import util
util.publish()
```

<br>
<br>
<br>

### Reporting issues

Should you happen to find errors or would like to contribute material to this guide, you can:

1. Click on the `+` button to the right of each paragraph to add a comment
2. Register on [GitBook](https://www.gitbook.com/book/pyblish/pyblish-by-example) to edit this book directly.
3. Fork the [GitHub repository](https://github.com/pyblish/pyblish-by-example) and submit a pull-request with your changes.


<br>
<br>
<br>

### Content

Have a look to the left for a table of contents, and below for related topics in the forums.

> **Note:** The below content was written at various versions of Pyblish and may not include current best practices, but all remain forwards compatible with version 1.4.

>For example, `.set_data("key", "value")` has been superseded by `.data["key"] = "value"` but will still work with newer plug-ins.

**Intermediate**

- [Responsibility of Extractors](http://forums.pyblish.com/t/responsibilities-of-extractors/266/9)
- [Multiple families workflow](http://forums.pyblish.com/t/multiple-families-workflow/205)
- [Per task plug-ins](http://forums.pyblish.com/t/task-specific-plugins/127)
- [Publishing with comments](http://forums.pyblish.com/t/publishing-with-comments/120)
- [Instances and Plain-Old-Data](http://forums.pyblish.com/t/instances-and-plain-old-data/136)
- [Cooperative Collection](http://forums.pyblish.com/t/cooperative-collection/137)
- [Search and Customisation](http://forums.pyblish.com/t/pyblish-search-and-customisation)
- [Good to know about Pyblish](http://forums.pyblish.com/t/good-to-know-about-pyblish)
- [`hosts` Attribute In-Depth](http://forums.pyblish.com/t/the-use-of-hosts-attribute/78/3)
- [Registration versus families](http://forums.pyblish.com/t/filtering-collected-instances-based-on-category-family/245/5)
- [Backwards compatibility](http://forums.pyblish.com/t/backwards-compatibility-and-breaking-changes/246)

**Advanced**

- [Magenta development thread](http://forums.pyblish.com/t/pyblish-magenta/79)
- [Developer Guide](http://forums.pyblish.com/t/developer-guide)
- [Pyblish in 100 lines](https://pyblish.gitbooks.io/developer-guide/content/pyblish_in_100_lines.html)

<br>
<br>
<br>

**Changelog**

- `2015-08-06 16:27` - Added [Quickstart](http://forums.pyblish.com/t/learning-pyblish-by-example/108/3)
- `2015-08-07 10:12` - Added [Architecture](http://forums.pyblish.com/t/learning-pyblish-by-example/108/6)
- `2015-08-07 10:14` - Updated [Quickstart](http://forums.pyblish.com/t/learning-pyblish-by-example/108/3)
- `2015-08-07 19:17` - Added [Good to know about Pyblish](http://forums.pyblish.com/t/good-to-know-about-pyblish)
- `2015-08-07 20:41` - Updated [Architecture](http://forums.pyblish.com/t/learning-pyblish-by-example/108/6)
- `2015-08-07 20:48` - Updated This
- `2015-08-09 10:51` - Updated [Validating II](http://forums.pyblish.com/t/learning-pyblish-by-example/108/16) with flow chart
- `2015-08-09 17:24` - Updated This, with installation instructions
- `2015-08-10 09:00` - Updated This
- `2015-08-11 07:28` - Updated [Quickstart](http://forums.pyblish.com/t/learning-pyblish-by-example/108/3)
- `2015-08-11 07:30` - Updated [Files](http://forums.pyblish.com/t/learning-pyblish-by-example/108/4) with comma-separated paths
- `2015-08-11 07:40` - Fixed typo in [Report IV](http://forums.pyblish.com/t/learning-pyblish-by-example/108/26)
- `2015-08-13 21:08` - Updated [Report I-IV](http://forums.pyblish.com/t/learning-pyblish-by-example/108/26)
- `2015-08-14 09:26` - Updated [Report I-II](http://forums.pyblish.com/t/learning-pyblish-by-example/108/26)
- `2015-08-18 07:02` - Added [host attribute in-depth](http://forums.pyblish.com/t/the-use-of-hosts-attribute/78/3)
- `2015-08-18 07:22` - Added "You will learn" to This
- `2015-10-19 14:38` - Updated use of "Asset" to "Instance"
- `2015-11-19 09:07` - Updated to pure-dict
- `2015-12-20 21:56` - Updated image of [Context + Instance](http://forums.pyblish.com/t/learning-pyblish-by-example/108/6).
- `2016-01-21 17:46` - Transitioned to GitBooks, removed section about custom test and services.
- `2016-06-07 09:48` - Defer use of GUI from guide.
- `2016-07-01 14:54` - Link to installation guide on Forum
- `2016-08-03 10:40` - Add intermediate and advanced links
- `2017-08-12 10:30` - Removed deprecated dependency injection link