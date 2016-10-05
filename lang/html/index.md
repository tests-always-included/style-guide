---
title: Style Guide for HTML
pageid: lang-html
keywords: 80 a about absolute after all allowed allows also alt always and angular anything apply appropriate are assets at atomic atomizer attach attribute attributes automatically available avoid be before being best better block br browser build by can capital capitalization characters checker child childnode childnodelist class close closing comment comments contain content contents correct css delivered description div do double-braces easily either element elements em embedded end enjoy entirely everything example explains extend external failing files flicker for from general generate guides hand have height here how html idx ie if img implicitly in include includes indent indentation indented index inline inline-block inside instead is it iterating javascript jquery js-cart-button js-checkout just label letters level libraries like line lines lint long lowercase may means ml-12 more moved my-custom-directive name names namespaced necessary newline newlines ng-bind ng-repeat no node nodes nor not of ok on ones or other out over override own p page possible process read reference referenced referencing rely right rules sample select selected selectors self-close separate set short should shown side site slash so something space spaces span specific specifically start still stripped style ta-c tag tags template test text that that's the their them themselves then there these this tidy to tool tooling trailing transformed try tt tt-u type unless uppercase urls use useful user using value values very via we when where which whitespace width will with within wrapped writing xhtml you z-5
---

These rules extend and override the [general rules][general-rules].  Also, the [CSS][lang-css] and [JavaScript][lang-js] style guides may apply.


Tooling
-------

If you are writing HTML by hand, use a lint checker.  About the best tool that's available is [HTML Tidy].

Use [Atomic CSS] when writing [CSS][lang-css], then use Atomizer to read the HTML and generate CSS automatically.


Capitalization
--------------

Everything within tags should be lowercase.  This includes the name of the element, attributes and attribute values where appropriate.  Capitalization is allowed for class names specifically for Atomic CSS.

Text that should be entirely uppercase should be transformed via [CSS][lang-css], do NOT JUST TYPE IN CAPITAL LETTERS.


Comments
--------

Comment anything that's useful.

Comments should be stripped out in a build process.  Do not rely on them being delivered to the browser.

All comments will be on their own line.  Long comments have the start and end tags on separate lines with the contents indented.


Elements
--------

Use XHTML style elements.  This means you include closing tags for tags that do not implicitly self-close.  For ones that do close by themselves, you include a trailing slash.  Example: `<span class="tt-u">Test</span>`, `<br />`.

Attributes have spaces before the attribute name.  There will be no space on either side of the `=` nor inside the value unless necessary.

Tag specific rules:

* `a`: Always set the `alt` attribute.
* `img`: Always set the `width` and `height` attributes.
* `label`: Set the `for` attribute so the right element is selected, or have the tag contain the element to select.

When referencing URLs for assets, use absolute URLs when possible.  That allows the page to be more easily moved on a site and still reference the correct libraries or content.


Indentation and Whitespace
--------------------------

Block and inline-block elements will always have a newline and indent the content within.

Newline after `<br />` tags.

No other newlines.


JavaScript and CSS
------------------

Do not attach JavaScript inline on elements.  Instead, try to use Angular.  Failing that, use something like jQuery and namespaced selectors selectors (ie. `.js-cart-button` or `.js-checkout`).

CSS and JavaScript should be referenced from external files, not embedded.


Sample HTML
-----------

    {% comment %} Wrapped in "raw" for Kramdown {% endcomment %}
    {% raw %}
    <div>
        <!-- Here is a short comment. -->
        <span>This is not a block level element</span>
    </div>
    <!--
        This is a very long comment which explains how we are iterating over the
        child nodes.  It is wrapped at 80 characters and the tags are on separate
        lines.
    -->
    <div class="ta-c z-5 ml-12" ng-repeat="childNode in node.childNodeList index by idx" my-custom-directive="childNode">
        <p>
            Using Angular double-braces is ok when the HTML is a template.
        </p>
        <div>
            {{childNode.name}}
        </div>
        <p>
            It is better to use <tt>ng-bind</tt> when the HTML may be shown
            to the user.  This can avoid the flicker.<br />
            Enjoy the <em><span ng-bind="childNode.description"></span></em>!
        </p>
    </div>
    {% endraw %}


[HTML Tidy]: http://tidy.sourceforge.net/

{% include links.html %}
