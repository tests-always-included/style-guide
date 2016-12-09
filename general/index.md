---
title: Style Guide for General Programming
permalink: /general/
pageid: general-rules
keywords: 123 4 8 80 a above acronyms act after afterwards all allow allowed alphabetically alphabetization also alternate always an and another any anything anywhere apart are as at attempt bad basis be because before better bin binary blank block blocks body boms brace braces break brief but by byte c call called can case characters checkers choice class close code codebase command commands comment comments complexity condition config configuration consider constructs contain control controlled convention copying correctly creating cyclomatic declarations decouple dedicated defaults dependencies dependency dependent describe directories directory do doc documentation each earlier easy editorconfig elements else employed encoding end environment escape example examples exceptions execute executed exercise existing exists exit expected extension extra fact fakefunction fakefunction2 fakefunction3 fashion feature file files fine first flag flow followed following for formats from function functions git go good guides handled happen hard hardcoding has have headings helpful-info helps here how html htmlparser html-parser hyphenation hyphens if ignore in increasing indentation individual initialisms injection in-place inside install installation installs instance intended is it item it's javascript js json keyword language language-specific last later level library license life like line lines lint lists local localization logical lowercase make makefile many marks may md means methods module modules monday moo moose mop more must my-tool name named names necessary need newline newlines no node_modules normal not note npm objects of off offset omit omitted on one ones only open or order ordered ordering other our out over overridden overriding package parent parses pep per performing placed please possible prefer primary procedure program programs project projects properties provide pull purposes python readme remove removed repository rest return root rules same sample scenarios script section sections send-message separate set sh shall shell shoehorn should shown similar single singular situations so some something some-value sorted space spaces specific standard statements such sure symbols syntax system t tab tabs test test_condition testing tests that that's the their themselves then there there's these they thing things this those throw to together tooling tools treated tricky try two types typical unix-style unless up urls use used user using usr utf-8 var variable variables version way we well what when whenever while whitespace will wish with within words working works would wrapped write writing written xyz yes you your
---

These rules are the basis for the rest of the guides.  These are the defaults and may be overridden as necessary.  Please note that we will prefer to use a language-specific standard when one such standard exists, such as PEP 8 for Python.


Tooling
-------

Life is better when tools do things for you.  You should use lint checkers and syntax checkers whenever possible.  When code is written, the standard tools for testing that code should be employed.

When possible, use [EditorConfig](http://editorconfig.org/).  Many of the whitespace rules can be handled by a single config file.  When creating a file, make sure that you flag it as the root of the project.  We have a sample [.editorconfig](editorconfig.txt) file that works well with many types of projects.

[Git][topic-git] is our version control system of choice.


Files, Encoding, Formats
------------------------

All files use UTF-8.  The files themselves shall not have byte order marks (BOMs).

Unix-style newlines will be used.

Files shall be named using all lowercase and with hyphens.  For example, `examples/send-message.js`.  Programs that are intended to be executed will omit their extension when they are in-place.  So, for JavaScript, a project may have `bin/my-tool.js` in the repository, but when `npm` installs the binary it is expected to end up as `my-tool` (that's controlled by the `package.json`).  Another example is when working with a shell script; it is fine to name the shell script `xyz.sh` in the repository, but the installation procedure for the script should remove the extension when it is placed in `/usr/local/bin/xyz`.

Directories also will be named in all lowercase and with hyphens.  Directories will be named in a singular fashion; they are named after what a single item within will provide.  So, `user/123.json` and `doc/helpful-info.md`.

The exceptions to the file and directory names are when there's an existing convention.  For example, the following things are allowed:  `README.md`, `INSTALL`, `COPYING`, `LICENSE`, `Makefile`, `node_modules/`.

Files will contain only one library, one class, or one feature.

For hyphenation purposes, acronyms and initialisms are treated as single words.  Your file that parses HTML may be called `html-parser.c` and it's primary function would be `htmlParser()`.


Indentation and Whitespace
--------------------------

Use 4 spaces per indentation level.

No spaces at the end of any line.

No tabs allowed anywhere.  If you wish to use a tab, escape it.  For instance, in JavaScript you would use `"\t"`.

The last line in a file shall have a newline after it.

Logical blocks are sections of code that execute together, such as a function or the body of `if` and `while` statements.

When braces are used in a language, those braces will be on the same line as the `if` or the function.  They will have a space before open braces.  If the close brace is followed by a keyword then it shall also have a space afterwards.

    fakeFunction() {
        if (test_condition) {
            code here
        } else {
            alternate code
        }
    }

Logical blocks will be offset by one blank line.  This is to call out that you are increasing the cyclomatic complexity.  The extra line will be omitted when the logical block is the first or last thing inside of another block.

    fakeFunction2() {
        while (condition) {
            no whitespace before this block because it is the
            first thing in the function
            Yes, whitespace afterwards.
        }

        some command
        more commands

        if (condition) {
            Whitespace before to separate it from other code.
            No whitespace afterwards because it is the last thing
            in the parent block.

            return some-value;
        }
    }

As shown in the above example, things like `return`, `exit`, and `throw` should be offset by a line as well.  They break typical program flow and the whitespace helps to call out that fact.


Comments
--------

Comments will be on the line before code.  Comments will be offset from any code above it by one line.  The blank line will be removed if the comment is the first thing in a block.

    fakeFunction3() {
        // This comment has no whitespace before it because it
        // is the first thing in a logical block.
        do something tricky

        // This comment has whitespace before it.
        do something else that is tricky

        return "this also has a blank line before it"
    }

To set functions off from other code, two blank lines shall be used.  To set sections apart from each other in documentation, two blank lines will be used before headings.  Also, variable declarations and return statements should be offset from normal code by a blank line.

Comments will be wrapped at 80 characters unless it is necessary to go over, such as when writing URLs.


Ordering
--------

Properties in objects, class methods, variable declarations, variables from dependency injection, and other similar lists will be ordered alphabetically when possible and when there's no overriding need to do it another way.

When there are no other dependencies on other functions, individual functions in a file will be ordered alphabetically.  When your functions in a module call each other, the dependent ones must be placed earlier.

When performing alphabetization, ignore symbols and ignore case.  That means these elements are sorted correctly:

    global $monday, Moo, moose, _mop;


Specific Constructs
-------------------

Try to pull in configuration from a config file or the environment.  Hardcoding anything is bad.

Attempt to allow for localization in the codebase.  It's hard to shoehorn that in later.


Tests
-----

There's a section dedicated to [writing tests][topic-tests].  In brief:

* Always consider how easy it is to write tests for your code.  This helps you decouple modules.
* Write good tests that exercise code whenever possible.
* Try to test scenarios.  Tests can also act like documentation and describe what would happen in specific situations.


{% include links.html %}
