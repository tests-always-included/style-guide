---
title: Style Guide for YAML
pageid: lang-yaml
---

These rules extend and override the [general rules][general-rules].


Whitespace and Indentation
--------------------------

YAML is fairly straightforward.  The only odd thing is when you embed objects in an array.  Use the expanded form as is illustrated below.

    name: YAML Example
    items:
        -
            name: First object
            favorite: true
        -
            name: Second object
            favorite: false


{% include links.html %}
