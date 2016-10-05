---
title: Style Guide for Python
pageid: lang-py
keywords: 0 120 2 4 6 80 a after an and are automatically available avoid bad base blocks by can changing checks class classes code come comprehension comprehensions config configure constructs contain contents creating default defining developers dictionary do doc double editing editor enforces exception extend files flake8 following for format functionality general globally good google's have hello im_smart in index install instead is it language length line list make makes max-line-length moving myclass new not object of ok only other override parameter pep8 person pip plugin predictable python quality quotes reason respect restructuredtext rules %s set so specific standard string style sure that the these they this to tool tooling unless use using version way we which with without x x**2 you your
---

These rules extend and override the [general rules][general-rules].

We respect [PEP8](https://www.python.org/dev/peps/pep-0008/) unless we have a good reason for not following it.  For doc blocks we use [Google's version of reStructuredText](http://sphinxcontrib-napoleon.readthedocs.org/en/latest/example_google.html).


Tooling
-------

Flake8 is a code quality tool which enforces the PEP8 standard.  You can install it globally using

    pip install flake8

After that, make sure to install a plugin so your editor automatically checks files for you.

The only exception to the base flake8 rules is the line length, which we set to 120 instead of the default 80.  You can configure this by
editing/creating `~/.config/flake8` and changing the contents to contain this:

    [flake8]
    max-line-length = 120


Specific Constructs
-------------------
 
Use [new style classes](https://www.python.org/doc/newstyle/).  They come with new functionality and it makes the code base predictable for other developers

    # GOOD
    class MyClass(object):

    # BAD
    class MyClass:

Use [string.format](https://docs.python.org/2/library/stdtypes.html#str.format).  It is the way the language is moving.

    # GOOD
    "Hello, {0}".format(person)

    # BAD
    "Hello, %s" % person

Use double quotes (").

Avoid [dictionary comprehension](https://www.python.org/dev/peps/pep-0274/).  It is not available in python 2.6.  [List comprehensions](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions) are ok.

    # BAD
    im_smart = {x: x**2 for x in (2, 4, 6)}

Do not use [string.format](https://docs.python.org/2/library/stdtypes.html#str.format) without defining an index for a parameter.

    # GOOD
    "Hello, {0}".format(person)

    # BAD
    "Hello, {}".format(person)


{% include links.html %}
