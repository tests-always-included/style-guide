---
title: Style Guide for Makefiles
pageid: lang-makefile
keywords: an and artifact as clean do extend for general lib list make not o override phony produce rf rm rules sure targets that the them these to
---

These rules extend and override the [general rules][general-rules].


Targets
-------

For targets that do not produce an artifact, make sure to list them as phony:

    .PHONY: clean
    clean:
        rm -rf lib/*.o


{% include links.html %}
