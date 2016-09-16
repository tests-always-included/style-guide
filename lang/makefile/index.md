---
title: Style Guide for Makefiles
pageid: lang-makefile
---

These rules extend and override the [general rules][general-rules].


Targets
-------

For targets that do not produce an artifact, make sure to list them as phony:

    .PHONY: clean
    clean:
        rm -rf lib/*.o


{% include links.html %}
