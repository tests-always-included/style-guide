---
title: Style Guide for Python
pageid: lang-py
keywords: 0 120 2 6 80 a after an and are automatically available avoid base blocks by can changing checks class classes code come comprehension comprehensions config configure constructs contain contents creating default defining developers dictionary do doc double each editing editor ending enforces exception exist extend files flake8 following for format functionality general globally good google's have hello in index install instead is it its language length line lines list make makes match max-line-length moving must myclass my_func_with_lots_of_parameters new not note object of ok on only order original other outdent override own param1 param2 param3 param4 parameter parameters parenthesis part pep8 person pip plugin predictable put python quality quotes reason respect restructuredtext rules separate set so specific standard start string style sure that the these they this to tool tooling unless use using version way we what when which with without work wrapping you your
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

    # Note the "(object)" part. This is what makes it a new style class.
    class MyClass(object):

Use [string.format](https://docs.python.org/2/library/stdtypes.html#str.format).  It is the way the language is moving.

    "Hello, {0}".format(person)

Use double quotes (").

Avoid [dictionary comprehension](https://www.python.org/dev/peps/pep-0274/).  It is not available in python 2.6.  [List comprehensions](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions) are ok.

Do not use [string.format](https://docs.python.org/2/library/stdtypes.html#str.format) without defining an index for a parameter.

    # Note the "0". This must exist in order to work with python 2.6.6
    "Hello, {0}".format(person)

When wrapping parameters on separate lines, put each parameter on its own line and outdent the ending parenthesis to match the start of the original line.

    my_func_with_lots_of_parameters(
        param1,
        param2,
        param3,
        param4
    )

{% include links.html %}
