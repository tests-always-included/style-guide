---
title: Style Guide for YAML
pageid: lang-yaml
keywords: an and array as below embed example expanded extend fairly false favorite first form general illustrated in indentation is items name object objects odd only override rules second straightforward the these thing true use when whitespace yaml you
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
