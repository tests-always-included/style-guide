---
title: Style Guide for CSS / LESS / SASS
pageid: lang-css
---

These rules extend and override the [general rules][general-rules].


Tooling
-------

If you are writing CSS by hand, use a lint checker.  We recommend [PrettyCSS].

When possible use [LESS].  If not, use [SASS] or fall back on vanilla CSS.  LESS has interpreters written in several languages where as SASS is only in Ruby.  Plain CSS is simply prone to errors.

Use [Atomic CSS] when writing [HTML][lang-html], then use Atomizer to read the HTML and generate CSS automatically.


Rules
-----

When styling, only use classes.  Never use inline styles nor IDs.    Do not reuse class names.

If you have special CSS for a particular template (though that is extremely unlikely unless you are developing a library) it must be broken out into a separate file.  Name the file the same name as the class and namespace all of your styles under that class.  Your parent element for the template should contain the namespace class (eg. `<div class="template">`) and all of your generated styles will have a selector with the namespace, like `.template .whatever { ... }`.

There should be no need to have multiple selectors on a single line.  When you do, separate the selectors by newlines.

    /* Incorrect */
    body, html {
        zoom: 1
    }
    
    /* Correct */
    body,
    html {
        zoom: 1
    }


Specificity
-----------

Be *very careful* with specificity.  We aim to have rules with extremely low specificities.

Namespace the atomic CSS under `body` to give it a specificity of 0,0,1,1.

A separate "theme" set of styles should be made in order to generically style specific bits.  Their specificity should be 0,0,1,0 so that the atomic CSS will override it.

Never use inline styles because they mess up the specificity.

Never use `!important` because they mess up the specificity.

Never style by IDs because they also mess up the specificity.  Additionally, one is supposed to honor that IDs can occur only once on a page, but that's not enforced anywhere.

Never style based on HTML element structure because that's more brittle than styling the element directly.


Variables and Class Names
-------------------------

Create a set of variables that describe the theme being used (colors, fonts, etc) and use those variables in all of the rules.  Make sure the variables describe how the color/size is used such as `important-text-color` and `sidebar-background-color`.  Do not use its value, like `green-text`.  Do not use any hardcoded colors.

Styles used for the theme should be all lowercase and hyphenated, such as `legal-text` and `advertiser-image-caption`.  CSS is case insensitive, but HTML selectors (like what's used in JavaScript to find elements) is case sensitive.

If some class is intended to be used by [JavaScript][lang-js], give it a `js-` prefix and only use that class with JavaScript.  If you need to also style it, give that element multiple styles.  For instance, `js-order-subtotal order-subtotal` is valid.

Class names should be listed alphabetically in a file.  That means the rules for `external-link` should appear before before `internal-link` in the CSS.

Typically the values should not use `em`.  Prefer `px` or `pt`.  When using hex color codes, use lowercase.


Comments
--------

Comments are wonderful.  Make sure that you only use `/* comment */` style comments.  The CSS spec only allows comments *between* things, not within a property definition.  Add them before or after (but not within) properties and rules.

    /* This is a valid location for a comment */
    .some-class /* Invalid! */ {
        /* Good spot */
        float: /* Invalid! */ left;
    }

Comments will also have a newline before them to make them visually stand out from other properties.  This is discussed further in the [general rules][general-rules].

Comments should be stripped out during the build process.


Indentation and Whitespace
--------------------------

Properties will have no space before the colon and exactly one space after.  The property's value will always be followed by a semicolon.


Reset vs Normalize
------------------

We use neither.  Instead, we have a pretty minimal [reset.css](reset.css).  We encourage you to use it.


Example
-------

`palette.less`:

    /* The palette is all of the colors and fonts that should be used.
     * Typically this is given by the UI team when they create the final
     * designs.  These settings should be used throughout the site.
     */
    $legalTextColor: black;
    $sidebarBackgroundColor: #D0D0D0;

`theme.less`:

    /* The theme file lists broad groups of styling that can be applied
     * to elements.  Each of these can be overridden by specifying Atomic
     * CSS rules on elements.  This works best because of the low
     * specificity of these rules.
     */
    @import "palette.less"

    .legal-text {
        /* The general rules says to list properties in alphabetical order */
        color: $legalTextColor;
        font-size: 8pt;
        font-style: italics;
        text-transform: uppercase;
    }

    .sidebar {
        background: $sidebarBackgroundColor;
        float: right;
    }


[Atomic CSS]: http://acss.io/
[LESS]: http://lesscss.org/
[PrettyCSS]: https://github.com/fidian/PrettyCSS
[SASS]: http://sass-lang.com/

{% include links.html %}
