---
title: Style Guide for CSS / LESS / SASS
pageid: lang-css
keywords: !important #343434 #d0d0d0 $legaltextcolor $primarytextcolor $sidebarbackgroundcolor 0 1 8pt @import a add additionally advertiser-image-caption after aim all allows alphabetical alphabetically also always and another any anywhere appear applied are as atomic atomizer automatically back background based be because before being best between bits black block body brittle broad broken build but by can careful case checker class classes codes colon color colors comment comments contain correct create css definition denoting describe designs developing directly discussed div do during each eg element elements em encourage enforced errors etc exactly example extend external-link extremely fall file final find float followed font-size font-style fonts for from further general general-rules generate generated generically give given good green-text groups hand hardcoded has have hex honor how html hyphenated ids if important-text-color in incorrect indentation inline insensitive instance instead intended internal-link interpreters into invalid! is it italics its javascript js- js-order-subtotal lang-html lang-js languages left legal-text less library like line lines lint list listed lists location low lowercase made main make means mess minimal more multiple must name names namespace need neither never new newline newlines no nor normalize not occur of on once one only or order order-subtotal other out overridden override page palette parent particular plain possible preceeded prefer prefix pretty prettycss process prone properties property property's pt px read recommend reset reuse right ruby rules same sass says section sections selector selectors semicolon sensitive separate separating set settings several should sidebar sidebar-background-color simply single site size so some some-class space spec special specific specificities specificity specifying spot stand stripped structure style styles styling such supposed sure team template text-transform than that that's the their them theme then there these they things this those though throughout to tooling two typically ui under unless unlikely up uppercase use used using valid value values vanilla variables very visually vs we what what's whatever when where while whitespace will with within wonderful works writing written you your zoom
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

There will be one new line between styles, while there will be two lines separating style sections.  Style sections will be preceeded with a comment denoting what the section is for.


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
    $primaryTextColor: #343434;
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


    /* Another block of styles */
    .main {
        color: $primaryTextColor;
    }


[Atomic CSS]: http://acss.io/
[LESS]: http://lesscss.org/
[PrettyCSS]: https://github.com/fidian/PrettyCSS
[SASS]: http://sass-lang.com/

{% include links.html %}
