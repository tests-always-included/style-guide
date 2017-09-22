---
title: Style Guide for PHP
pageid: lang-php
keywords: 0 1 a above acceptable accidentally across addition after all allow all_uppercase_with_underlines also always an and another any apply appropriate appropriately are as attempt autoloaders avoid bad bar be because bit block braces built-in but by camelcase can can't capital cascading case cases cast casting casts catch cause certain checker class classes clean comes comments compound condition consider consistency constant constants constructs containing contains control correctly could count criteria csrf declaring defined describe designing do doc dofunction dothingie during each easy echo either elements elements0 eliminate else elseif empty enable end equality error evaluate even everyone example exception execution extend extra failure false file filename files findelements findorder folder folders foo for forcing format forms from function functions general get getting give global good goto habit happen has have helps hinting html hyphenated id if immediately implicit in include include_once includes indentation indicate indication information input inputs instance instead interface into is is_null issues it its javascript keep l latter leadingcapitals lib like likewise lines lint live loadorder log lowercase make makes many method methods mimics mind misspelled mistyped more must name named names naming need nested never not nothing null object occurs of often only or order orderdata other others override own parameter parenthesis pascal passed-in path php phpdoc possible prefer problems put quicker range rather really related repeating require require_once results return returned rules same selectorderfromdb separating set should shouldn't single single-quoted so someclass someclasstest something specific statements stream stream_input string strings structure structures subdirectory such sure t test testing tests text-transformations text-transformationstest than that the then these they things this those throw to tooling true two type typos under underscore unexpected unfortunate unless up usable use used user user-defined using util utiltest valid value values variables want warning warnings watch we when whenever where which whitespace whose will with won't work works would writing x y you your
---

These rules extend and override the [general rules][general-rules].  Likewise, PHP is often used with [HTML][lang-html] and [JavaScript][lang-js], so those rules also apply.


Tooling
-------

PHP has its own lint checker, `php -l FILENAME`.


Files and Folders
-----------------

Do not include a path when using `require()`, `require_once()`, `include()`, or `include_once()`. The include path should be set up appropriately so that the cascading of includes will happen correctly.  Prefer `require_once()` unless you must `include()`.  The other two shouldn't be used.

Files containing classes should be named `SomeClass.class.php` (not hyphenated, Pascal case).  This makes it really easy for autoloaders.

Files containing only functions should be named after the things it contains, such as `text-transformations.php`.

Files that are tests need to have `Test` in the name (with a capital T), such as `SomeClassTest.php` and `text-transformationsTest.php`.  They should be in a `test/` folder whose structure mimics where the files live.  For instance, if you have `lib/util.php` the test would be `test/lib/utilTest.php`.


Variables and Naming
--------------------

Functions and variables will use `$camelCase` format.  Built-in constants will be lowercase, like `true` and `null`.  User-defined constants will be `ALL_UPPERCASE_WITH_UNDERLINES`.

Class names use `LeadingCapitals`.  In addition, if the classes are nested under a subdirectory such as `lib/Stream/Input.class.php`, then the class name would have an underscore where the `/` is: `Stream_Input`.


Indentation and Whitespace
--------------------------

Do not use global variables.

All control structures will use braces and parenthesis.

    // Bad
    if ($condition)
        doFunction();

    // Good
    if ($condition) {
        doFunction();
    }

Attempt to not use compound statements. `if (($a = doThingie($x, $y)) == false)` is not as clean as separating that into two lines.



Comments
--------

Use [PHPDoc] to describe the file, which should either have related functions or a single class.  For each function, include another doc block.  Describe the inputs and return value.


Specific Constructs
-------------------

Use defined constants instead of repeating a string. It helps to eliminate typos because you will get a PHP warning when it comes across a misspelled constant, but a mistyped string won't cause any issues with PHP.

When designing a function, method, or class, make sure you keep the end user in mind. You want it to be easy to use by others, even if that makes a bit more work for you. The returned values should be immediately usable instead of forcing everyone else to do a bit of extra work to get usable information.

Use type hinting (for example, `function foo(Order $bar)`) whenever appropriate.  In this example, we are declaring that the passed-in parameter `$bar` must be an object which is an instance of class or interface `Order`.

Always return the same type from a function or method. To indicate nothing use `null`. If an error occurs during execution throw an Exception. In certain cases it also acceptable to return false.

    // Good
    function findElements($criteria) {
        $elements = {...}
        return $elements;
    }

    // Bad
    function findElements($criteria) {
        $elements = {...}

        if (count($elements) === 1) {
            return $elements[0]
        }

        return $elements;
    }

    // Good
    function findOrder($id) {
        $orderData = selectOrderFromDb($id);

        if (empty($orderData)) {
            return null;
        }

        return loadOrder($orderData);
    }

    // Bad
    function findOrder($id) {
        $orderData = selectOrderFromDb($id);

        if (empty($orderData)) {
            return $orderData;
        }

        return loadOrder($orderData);
    }

Many methods and functions return either a valid range, or `true`, `false`, or `null` as the failure indication. Use `===`, `!==`, `is_null()` rather than ==, !=, or !. The latter forms allow implicit type casting, and when the valid range could be cast to `false`, your test can give unexpected results.  For example, PHP casts string values to something unfortunate whenever possible.

    $string = '0';
    if ($string == false) echo "this works";
    if ($string == null) echo "this works";
    if ($string = true) echo "this works"
    if (!$string) echo "this works";

To avoid the above issues, consider getting in the habit of writing `if (false === $csrf)` rather than `if ($csrf === false)` when testing for equality.  This helps also when you use `if (false = $csrf)`; PHP will catch that error.

Never use `goto`.

Instead of `else if` use `elseif` for consistency.

Enable all warnings in PHP.  Watch the log and eliminate problems.

Use single-quoted strings.  You can't accidentally put in variables and they evaluate quicker.


[PHPDoc]: https://www.phpdoc.org/

{% include links.html %}
