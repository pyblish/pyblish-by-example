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
[API]: https://github.com/pyblish/pyblish.api/wiki

<br>
<br>
<br>

### Introduction

Pyblish is an open source, cross-platform framework designed for test-driven content creation.

*Pyblish by Example* is a hands-on introduction to Pyblish using short example programs, designed to read from top-to-bottom; like a book. 

- [What is Publishing?](https://github.com/pyblish/pyblish/wiki/What-is-publishing)


<br>
<br>
<br>

### How to use this guide

As you read through this guide, you can choose to use either the "core" library, consisting of a scripting- and command-line interface, or you can supplement your experience with a GUI; which is most like the actual experience of your users.


[pyblish-qml]: http://github.com/pyblish/pyblish-qml
[1]: http://forums.pyblish.com/t/learning-pyblish-by-example/108/2

<br>
<br>
<br>

### Reporting issues

Should you happen to find errors or would like to contribute material to this guide, see the parent GitHub project for more information.

- [Pyblish by Example on GitHub](https://github.com/pyblish/pyblish-by-example)


<br>
<br>
<br>

### Installation

If you haven't already, go ahead and install Pyblish for [Windows][w], [Linux][l] or [OSX][o].

- [Windows][w]
- [Linux][l]
- [OSX][o]

[w]: https://github.com/pyblish/pyblish-win/wiki/Installation
[l]: https://github.com/pyblish/pyblish-linux/wiki
[o]: https://github.com/pyblish/pyblish-osx/wiki

This will install both the scripting, command-line and graphical user interface. You can instead choose to install the bare essentials via `pip`.

```bash
$ pip install pyblish
```

This will install just the scripting- and command-line interfaces and occupies 1.17 mb of disk space (1.10 mb of which is vendor packages).

<br>
<br>
<br>

### Content

Have a look to the left for a table of contents, and below for related topics in the forums.

**Intermediate**

- [Install via Git](http://forums.pyblish.com/t/running-from-separate-repos/194/2)
- [Per task plug-ins](http://forums.pyblish.com/t/task-specific-plugins/127)
- [Publishing with comments](http://forums.pyblish.com/t/publishing-with-comments/120)
- [Dependency inject host](http://forums.pyblish.com/t/dependency-inject-host/102)
- [Instances and Plain-Old-Data](http://forums.pyblish.com/t/instances-and-plain-old-data/136)
- [Cooperative Collection](http://forums.pyblish.com/t/cooperative-collection/137)
- [Search and Customisation](http://forums.pyblish.com/t/pyblish-search-and-customisation)
- [Good to know about Pyblish](http://forums.pyblish.com/t/good-to-know-about-pyblish)
- [`hosts` Attribute In-Depth](http://forums.pyblish.com/t/the-use-of-hosts-attribute/78/3)


**Advanced**

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