---
title: Style Guide for JavaScript
pageid: lang-js
keywords: 0 1 100% 2 3 3rd 4 5 6 80 a abc-manager about above access accesses according achieve add added adds adhere after aim alert aliases all alongside alphabetical alphabetically already also alternative always amd amount +amount an and angular angular-specific annotations anonymous anotherclass~speciallyformattedobject any anything api apply are args arguments arrange array arrays arrayvar arrow as assign assigned assigning assignments assigns associated asterisks at attached automate avoid away back basic be because becomes been before beginning behavior behavioral between bigger bit bits blank block blocks bodies body boilerplate bool boolean both braces brackets branch branches break browser browsers bus but by call callcount calling calls camelcase can capital capitalization capitalized car care careful carefully case cases cast catch chained chaining change charactercount characters check checker checking checks class classes cleanliness closely code codes collection colon column come comma commas comment commented comments compare comparison compelling concat configuration conflict conform considered consistency console const constants constructor constructors constructs consumed contains content contents context control copy copyproperty correct could count counter coverage create created creates css current custom data +data dataname datatypes date datepicker-directive debuggable declaration declared declaring default define defining dependencies dependency describe describes description descriptions desired development different directives directly directories disable display displayable dizzy do documented documenting does don't double-quoted duck each early easier easy ecma eg either element elements else embedding empty enable encouraged end ending enforced entire entirely environment error es5 es6 eslint eslintignore eslintrc etc even event eventemitter every examine example examples exception exceptions executes expanded expected explain explaining export exports exportsname exposed extend factory fake faketestclass faketestdata false falsy far few fid-umd file filename files file's find first fit flags folder folders follow followed foobar for forced forces foreach formatted formatting former four from front function functions general get gets git global globals goes going grammatically guide handler has have having haystack ~haystack header help helps here hoisting however html if illustrate illustration illustrative immediately immediatly in include includes incoming increases increment increments indent indentation indexof indicate indicates indicating info informational injecting injection inline input inside instance instances instantiates instead intended intentionally interpreter into is isobject it item items iterates its it's itself javascript jquery jquery-ized js jsdoc json just keep know known last lastclickdata lastclickdataname latter leading leave left length less let letter letters lib libraries library lieu lifecycle like limit line lines lint linter list listed listing literal literals little live loading log logger logger~instance logs long looks loosely lot magic manager manual many markdown markup match matches matching matters may mentally merging message method methods method's minification minifier missing mistakes mode module module-constrained modulejs modules module-system-agnostic more most mousex mousey much multiple must myclass name named names naming nan near neat necessary need needed needle never new newline newlines newly next no node~console nor normally not notable notes nothing null +num number object objects observable of off often omitted on onclick one ones only opening opentoken operates operators option optional optionally or order ordered ordering original other otherwise out outdent outside overridden override own package param parameter parameters parent parenthesis part party pass passed path pattern per perform picky placed possible post post-end prefer preferred pretty problem problems processentry programmers prohibited project prominent promise property property's prototype provide provided purpose purposes question quick quite quotes read reason recommend related removed repository require required resolve response-template-service response-template-service-declined restify return returning rewrite root rootname router rules run same sample samplemodule sanity scope script see semicolons sentence separate separates server services shall shorthand should shouldn't show showstrings signifies similar similarly simpler single single-line slice so some some-directive-service some-feature somefunction something sometimes sort sorted source sourced space spaces spec special specific specifically specifying split standalone standard start statements str strict string stringlist strings structures stuff style such suggest supersede supposed switch switches symbols syntax systems tags template ternary test testing tests text than thankfully that that's the thecontentwewanttoexport their them then there there's these they things think this those though through throughout thus to tooling top total touppercase trailing tricky trivial true truly try two type typecasting typecasts typed typedef typeof types typical typically typing ugly umd unacceptable undefined underscores un-indented unless unquoted unsent unshift unused up upper uppercase url us usage use used user uses using usually utilizing value values var variable variables very via vs want wary way we well were we're what whatever when where which whitespace will wind window wish with within without wording work working works would wrap wrapping write writes writing written x y yaml yname you your yourself yui zero
---

These rules extend and override the [general rules][general-rules].

If you are writing Angular code, adhere to the [Angular 2 Style Guide] or the [Angular 1 Style Guide].  Their rules will supersede these.


Tooling
-------

Use a lint checker.  We recommend [ESLint].  We also have a custom [.eslintrc.yaml](eslintrc.yaml) and [.eslintignore](eslintignore.txt) for general purpose JavaScript utilizing ES6.  When writing code for Angular, you may prefer this [.eslintrc.yaml](eslintrc-angular.yaml) for Angular.  The rules are quite strict intentionally.  We aim to catch as many problems as possible early in the development lifecycle.


Files and Directories
---------------------

Tests for `*.js` files are named `*.spec.js`.  It is preferred that tests live within a `spec/` folder in a path that otherwise matches the original filename.  For instance, when testing `lib/manager/abc-manager.js`, the test filename will be `spec/lib/manager/abc-manager.spec.js`.  Sometimes, such as with Angular code, tests live alongside the libraries.

Angular directives, services, etc. have their type after the name (eg `some-directive-service.js` and `datepicker-directive.js`).  Angular code, in general, will be within folders for each module.

Files closely associated with each other should be named similarly.  This way you can see that the files `response-template-service.js`, `response-template-service.css` and `response-template-service-declined.html` are all related.

See [a suggested app structure here](suggested-app-structure.md).


Variables, Naming and Capitalization
------------------------------------

Do not use global variables.

There shall be a single `var` line per function.  Optionally, there may be a `var` line near the top of a file for module-constrained "global" variables.  There will be a single `const` declaration for constants used in a module.

Variables, methods and property names will use `camelCase` style formatting.  Only constructors will use a leading capital letter, such as `Date` and `EventEmitter`.  Underscores are prohibited.

Functions are named only if they are not supposed to be overridden.  Anonymous functions do not need a name and shouldn't get one and should either be passed directly or assigned to a variable.

When declaring multiple variables, they should be declared alphabetically and any symbols at the front of variable names should come before ones without. This is enforced with the ESLint configuration we use. Where there is a conflict between two matching variable names, capitalized variable names should be listed first; think carefully before you name two variables similarly because that typically indicates a problem.

It is typical, when using jQuery, to name your jQuery-ized variables with a `$` in front, like `$elements = $('input');`.


    // Alphabetically Correct
    function someFunction () {
        var $car, bus, Car, car;

        // Work here
    }


Comments
--------

Comment any tricky bits of code or rewrite them entirely to be less tricky.

Use `//` style comments for single lines and `/* comment */` style for multiple lines.  For multiple line comments, there should be a column of asterisks that line up.  The comment must be placed before the code in question.

    // This bit is tricky - we don't call the function
    if (foobar) {
        /* A bigger comment goes here for an example.
         * We're calling foobar in a special way.
         */
        foobar.call(foobar);
    }

Use `/* eslint some-feature:"off" */` style comments for eslint flags.  Disable the check for as few lines of code as possible.

Use `/* global someThing */` style after the file's JSDoc header for defining global variables for eslint.  However, this should not be necessary because we should be using factory methods and injecting dependencies.  A notable exception is when working with JavaScript that operates in a browser and 3rd party libraries are exposed only through global variables.

Comments wrap at 80 characters unless there's a compelling reason not to do this, such as when using a very long URL or embedding a code example.

Never leave code that is commented out.  It should be removed.  If we need it back, the code should all be documented through [git][topic-git].


JSDoc Comments
--------------

JSDoc is required before every function and at the top of a file in order to explain the purpose and usage.

JSDoc comments start with `/**` on a line by itself.  The first line should be a single-line quick description and is followed by an empty line.  After that is an optional description and [Markdown][lang-md] is encouraged.  A newline separates description from parameters or other annotations.  Use `@param` and `@return` instead of the aliases.  When documenting a `Promise`, indicate the value that will be provided if the promise is resolve.

`Array` and `array` are two different things.  The former is an object and the latter is a basic data type.  It's more prominent if you are using `String` vs `string` or `Boolean` vs `boolean`.


Indentation and Whitespace
--------------------------

The [general rules][general-rules] has most of these rules.

Opening braces and brackets are attached to the code on the left.  Indentation always increases with braces and arrays.  Spaces before and after most operators.  Blank line above comments, two blank lines above JSDoc comments.  No whitespace required at the very beginning nor end of a block of code.  Newlines after commas in a list of constants, array literals and object literals.  No space between a function name and its arguments.  Include a space after operators.

ESLint forces `case` statements and the `default` case in switches to be un-indented (just that line).  There must be a blank line after `break;` as well.

Chained function calls will be on one line, specifically because the linter will get picky when you try to pass an object literal as a parameter.  It will want you to not indent the chained function call or outdent the object literal, both of which are more unacceptable than having a very long line of chained methods.  This intentionally looks ugly so you write code that's more debuggable.  Alternative methods would be to limit chaining, pass in variables instead of object literals, and assigning a newly created object to a variable before calling a method on it.

No other newlines.

Property names shall be followed immediately by a colon, a space, and the property's value.


ES6, ES5
--------

No trailing comma after the last property of an object or the last element in an array.

We typically code for ECMA Script 6.  Notable exceptions include libraries that could be used in browsers or Angular code.  In those cases we conform to ES5 entirely; the tests may run in an ES6 environment but the entire repository should use ES5 style for consistency.

JavaScript that is expected to work outside of Angular is written using a module loading syntax.  Angular-specific code already uses a module syntax.  For module loading we suggest [Dizzy] or [ModuleJS].  If this is going to work in a browser, you should check out [Fid-UMD] to package source files in a module-system-agnostic method.

When writing ES6, use arrow functions for anonymous function unless you must use a different context (the `this` variable) or if you want to access the magic `arguments` variable.

We like parenthesis and braces.  All control structures, like `if` statements, require braces.  ES6 arrow functions should use parenthesis, braces and `return`.


Specific Constructs
-------------------

Property names should be unquoted unless it is necessary to wrap them in quotes.

Nothing that's displayable to the user should be sourced from JavaScript.  The wording should come from an HTML template, a JSON file from a server or API calls.  Provide codes, not text strings.

Use double-quoted strings.

Avoid manual minification - let a minifier do it.  Ternary statements should be expanded into `if` blocks.  Even though `!!~haystack.indexOf(needle)` is tricky and neat, write `haystack.indexOf(needle) !== -1` so all programmers on the project immediatly know what the code does.

Typecasting can use a little bit of shorthand.  `+num` to cast to a number or `NaN`, `+num || 0` to cast to a number (`NaN` becomes 0), `!!bool` to cast to a boolean, `[].concat(arrayVar)` to cast to an Array.

Because JavaScript is loosely typed, `5 == "5"` is true.  If you need to care about data types, you can compare them with `5 === "5"`.  This matters a lot for falsy values such as `null`, `undefined`, false, 0, and "".

* `null` is an empty value and it's a "known" empty value.  Not an error.
* `undefined` is an empty value that usually signifies a missing return value, parameter or unsent data.  If we assign it to something it should be considered some sort of error.
* `false` is a boolean indicating something is off.
* `0` is the number zero.
* `""` is an empty string.

To compare these things we typically will use `if (!variable)` instead of `if (variable === false)`.  When we must care about datatypes, we are (thankfully) forced by ESLint to use `===` and `!==`.  Be wary of `switch` because its comparison is **not** loosely typed.

For easier testing and much more sanity, follow a dependency injection pattern and have all of the library files export a function, then call the function to pass in dependencies.  [Dizzy] can automate this, such as with the [OpenToken] repository, though you can just do the dependency injection yourself like [Restify Router Magic].

Always use semicolons.  ESLint helps find mistakes where they were omitted.

Prefer duck typing in library functions unless you truly care about using specific types of instances.  In tests, it is often simpler to perform instance checking.


Ordering
--------

File contents are ordered according to the type of content that is within the file.  Classes are also ordered and functions have their own special notes as well.


### Modules (Collection of Functions)

    /**
     * This file is an example module.
     */
    "use strict";


    /**
     * Change a string into uppercase.
     *
     * @param {string} input
     * @return {string}
     */
    function upper(input) {
        return input.toUpperCase();
    }


    module.exports = upper;

1.  JSDoc comment explaining the scope of the code.
2.  Enable strict mode with `"use strict";`
3.  Functions that should be used throughout.
4.  Class declaration, if needed.
5.  Assign the class, function, or object to `module.exports`.


### Modules (Factory Function)

When using a factory, the order is the same, however the factory function typically contains all of the necessary functions.

    /**
     * This file is an example that exports a logger factory.
     *
     * The factory pattern helps us avoid using global variables.
     */
    "use strict";

    /**
     * Creates the logger.
     *
     * @param {node~console} console
     * @return {logger~instance}
     */
    module.exports = () => {
        /**
         * Logs an informational message to the console.
         *
         * @param {*} ...args
         */
        function info() {
            var args;

            args = [].slice.call(arguments);
            args.unshift("INFO:");
            console.log.apply(console, args);
        }


        /**
         * @typedef {Object} logger~instance
         * @property {Function} info
         */
        return {
            info
        }
    }


### Library for Multiple Module Systems

If your code is intended to be consumed as a library, the order is similar.

    // fid-umd {"name":"SampleModule"}
    (function (name, root, factory) {
        function isObject(x) { return typeof x === "object"; }
        if (isObject(root.module) && isObject(root.module.exports)) {
            root.module.exports = factory();
        } else if (isObject(root.exports)) {
            root.exports[name] = factory();
        } else if (isObject(root.define) && root.define.amd) {
            root.define(name, [], factory);
        } else if (isObject(root.modulejs)) {
            root.modulejs.define(name, factory);
        } else if (isObject(root.YUI)) {
            root.YUI.add(name, function (Y) { Y[name] = factory(); });
        } else {
            root[name] = factory();
        }
    }("SampleModule", this, function () {
        // fid-umd end

        "use strict;"

        // Do stuff here

        return theContentWeWantToExport;

        // fid-umd post
    }));
    // fid-umd post-end

1.  JSDoc comment explaining the scope of the code.
2.  [Fid-UMD] markup and wrapping code.
2.  Enable strict mode with `"use strict";`
3.  Functions that should be used throughout.
4.  Class declaration.
5.  Return the desired value.
6.  [Fid-UMD] ending wrapping code.


### Class Bodies

A class body is also ordered.

    /**
     * A trivial counter example.
     */
    class MyClass {
        /**
         * Creates the object.
         */
        constructor() {
            this.value = 0;
        }

        /**
         * Increments the value by an optional amount.
         *
         * @param {number} [amount=1]
         */
        increment(amount) {
            if (typeof amount === "undefined") {
                amount = 1;
            }

            // Careful.  This typecasts intentionally.
            this.value += +amount;
        }

        /**
         * Logs the current value.
         */
        log() {
            console.log(this.value);
        }
    }

1.  JSDoc comment explaining the class.
2.  Class declaration.
3.  Constructor (if any).
4.  Alphabetical listing of methods.
5.  Assign the object to `module.exports`.


### Function Bodies

Function bodies also have a specific order.  This helps to mentally arrange items to match the hoisting that the interpreter uses.

    /**
     * Example function that iterates through an array.
     *
     * @param {Array.<string>} stringList
     * @return {number} Total number of characters.
     */
    function showStrings(stringList) {
        var characterCount;

        /**
         * Writes a single item to the console.  Adds the number of
         * letters to characterCount.
         *
         * @param {string} str
         */
        function processEntry(str) {
            characterCount += str.length;
            console.log(str);
        }

        stringList.forEach(processEntry);

        return characterCount;
    }

1.  JSDoc comment explaining the function.
2.  Function declaration.
3.  Variable declaration.  One line only, alphabetical variables, no assignments.
4.  Functions, sorted alphabetically when possible.
5.  The code that executes.


Testing
-------

You can and should achieve 100% test coverage and examine all branches.  It's far easier when you use a factory pattern for your libraries.

We wish to perform behavioral testing.  Test every intended way we will be using objects and all exposed functions.

All tests should pass before merging code to a parent branch.

Test names should be grammatically correct and read like a sentence.  The descriptions should describe the observable behavior, not what is going on in the code.


Example
-------

This example is quite long and includes many comments to help illustrate the rules.

    /**
     * This is a JSDoc formatted comment that describes the file.  Not much is
     * expected here as far as annotations.  The lines all fit within 80
     * characters and the asterisks on the left all line up.  Markdown is
     * expected to be used for code examples, but that's pretty easy.  Just
     * indent some code with four spaces and keep it a line away from text.
     *
     *     // Sample usage
     *     var test;
     *     test = new FakeTestClass();
     *     test.run('something');
     *
     * This next "global" part flags `window` as a global variable.  This
     * module will get `window` passed in as the `wind` parameter.  Nothing
     * in this function accesses any globals.
     */
    /*global window*/
    (function (global, wind) {
        /**
         * This is a fake class for illustration purposes.
         *
         * The class gets a capital letter at the beginning because it is a
         * constructor.
         *
         * @class FakeTestClass
         */
        class FakeTestClass {
            /**
             * Instantiates the object.  Assigns the call count property.
             * No arguments and no return code, so those JSDoc tags are not used.
             */
            constructor() {
                this.callCount = 0;
            },


            /**
             * Sample event handler
             *
             * @param {Event} event Unused in this example
             * @param {AnotherClass~speciallyFormattedObject} data Checks for callCount
             */
            onClick(event, data) {
                var lastClickData;


                /**
                 * Copy a property from incoming data into the lastClickData
                 *
                 * This is a function, thus it's split out here and documented.
                 * In lieu of this separate function, an ES6 arrow function
                 * could have been used inside the `.forEach()`.
                 *
                 * @param {string} name
                 */
                function copyProperty(name) {
                    if (data[name]) {
                        lastClickData[name] = data[name];
                    }
                }


                if (typeof data === "object" && data.callCount) {
                    this.callCount = +data.callCount || 0;
                }

                lastClickData = {};

                /* Normally `copyProperty` would be an inline arrow function.
                 * It is a standalone function here for illustrative purposes.
                 */
                [
                    'mouseX',
                    'mouseY'
                ].forEach(copyProperty);
                lastClickData.fakeTestData = {
                    callCount: this.callCount,
                    instance: this
                };
                this.lastClickData = lastClickData;
            },


            /**
             * Run a test, display a message.
             *
             * The method's added to the prototype this way for cleanliness,
             * but using Object.create() is also an option.  The return value
             * is "this" so we are not specifying a type - it is possible that
             * the context is anything and we're returning whatever the context
             * is.
             *
             * @param {string} [message] Show this message via an alert
             * @return this
             */
            run(message) {
                if (message) {
                    wind.alert(message);
                }

                this.callCount += 1;
            }
        };


        /* Export to UMD or the global object - standard boilerplate.
         * This works as an example, but one should use Fid-UMD instead.
         */
        if (module && module.exports) {
            module.exports = FakeTestClass;
        } else {
            global.FakeTestClass = FakeTestClass;
        }
    }(this, window))


[Angular 1 Style Guide]: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md
[Angular 2 Style Guide]: https://angular.io/docs/ts/latest/guide/style-guide.html
[Dizzy]: https://github.com/tests-always-included/dizzy
[ESLint]: http://eslint.org/
[Fid-UMD]: https://github.com/fidian/fid-umd
[ModuleJS]: https://larsjung.de/modulejs/
[OpenToken]: https://github.com/opentoken-io/opentoken
[Restify Router Magic]: https://github.com/tests-always-included/restify-router-magic

{% include links.html %}
