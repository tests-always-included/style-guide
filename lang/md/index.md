---
title: Style Guide for Markdown
pageid: lang-md
keywords: 1 2 3 80-character a above after all also an and another are as at attempt attention avoid back bash be before beginning bin blank block blocks bulleted by can check code did directly document documentation documents echo enter example except extend fake fences flavored focus follow formatting four from general github grammar had have heading headings here html illustration in including indentation indented inserting instead is item it's length letters level limit line lines list lists long looks markdown markup match matched means miscellaneous most must my new newline newlines normal not notable now of on one only or other others over override paragraph paragraphs pay placed press resorting rule rules same sample script section see separate separates shell should single some spaces spell start subheading subheadings sublist sub-subheading symbols text that the there these thing things third this title to try two typical under use want we weirder when whitespace with without work you your
---

These rules extend and override the [general rules][general-rules].


Tools
-----

You can use [checkref](https://github.com/addaleax/checkref) to verify your markdown links work.  However, you need to load all of your markdown files in order to verify a single file, otherwise it will report all files as missing.

    checkref $(find -type f -name "*.md")


Formatting
----------

Follow the GitHub Flavored Markup.  The most notable rule there is you press enter when you want a newline.  That means paragraphs are over the typical 80-character limit.

Avoid inserting HTML directly.  Try to focus on documentation without resorting to HTML.

Use indentation instead of code fences.


Headings and Subheadings
------------------------

Documents start with a heading.  That should be the only one.  All others are subheadings.

Headings should use `======` and subheadings use `------` under the text.  The line of symbols should match the length of the letters.  Level 3 headings and on should use `#` at the beginning of the line.

    This Is An Example
    ==================

    This is some sample Markdown.


    Subheading
    ----------

    Did you see that the ==== and ---- matched the length of the heading?

    
    ### Sub-subheading

    Also pay attention to the newlines above all subheadings.


Indentation and Whitespace
--------------------------

All headings except the document title should have two blank lines before the heading and one after.

One blank line separates paragraphs, lists, code blocks, and other things.

Code blocks can not be placed directly after a list.  You must separate the list and the code block with a paragraph, heading, or another thing.

    * List item
    * Another list item

    Here is a code block as an illustration:

        This is a code block


Miscellaneous
-------------

Spell check and attempt to grammar check your work.


Example
-------

    My Sample Document
    ==================

    This is my sample document.  It's a long, single line.

    * My list item 1
    * My list item 2
        * Sublist item 1
        * These are indented with four spaces

    Including code in the bulleted list looks weirder.

    1. This is paragraph 1 of a list.

        This is paragraph 2 in the same list item.

    2. This is a new list item.

            This is a code block in list item 2.

    3. This is the third list item.

    Now we must use this paragraph to separate the list from code.

        This is a code block that is after the list.


    Section 1
    ---------

    This section had two blank lines before the title.

        #!/bin/bash
        # This is a sample code block and is indented by four spaces.
        echo "This is a fake shell script"

    And back to normal.


{% include links.html %}
