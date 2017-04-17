---
title: Test Quality
pageid: topic-tests
keywords: #2 $$childhead $apply $broadcast $child $compile $digest $new $parent $provide $q $rootscope $scope 'error' 'even' 'goahead' 'no 'number' 'odd' 'test'\ -1 0 1 100% 2 3 4 5 6 7 a ability able about above accomplishes achieve achieving acrobats action actions actual add added additional address adds afraid aftereach again against aim all allow allowed allownovalueevent allows already also alternate always am an and andreturn angular annoying another any anyone anything api app appears applies approach approaches appropriate are areas array arrow art as aservice aspects assert asserting assertions assume at attention audience avoid avoided back bad be because before beforeeach behavior being below better bit block blocks both branch branches broadcast broadcasting browser browsers bug bugfixes but button by cache call called calling calls can can't carefully carry case cases catch change changed changes check checked class clean clear cleared clearly click code combine combined coming common compatibility compile completely complexity complicated concerned confirm conflict consideration considered considering consistent content contradict contrived convenience converts convoluted correct could coverage createspy currently data decides default defects defer deferred define delete deleted depend dependency describe desired differ different difficulty direction directive directive's directives dirty disabled disallows distinct div do document does doesn't don't done doubles dozens duplicate duplicated each easier easy effects either element elements eliminate emit emits emitted emitting empty encounter ensure enter entire environment error errors especially essence even event eventdata eventemitted eventlist eventpassed events eventsemitted ever every everywhere exactly example examples exist expand expect expectations expected explain explorer extend eye failure false false? fast feed feel fickle field files filter find fire first fixed flow flowing follow for foreach form forms fragile frame frameworks free from front fulfilled function functional functionality functions future general general-rules get gets gives global go goahead goal good group grouping guarantee guess guidelines handle handled handling happen happened has have help here's hit how html i ian ian's identical if illustrate imagine implement important in include included independently indexof individual initial initialization inject injection input input\ inputs inside inspect installed instance instead intend intended interact interfaces interfere internal internals internet into invalid is isn't isolate isolated issues it it's item its itself jasmine jasmine-based job just know language last lastindexof later latter lengthy let's level levels lifetime like limit list listen listeners listening little lives load loading logging logic logical long longer look lot lower made maintainable make makes making many may maybe memory merely message method might mimic mind missing missing? mistake mix mixed mocks module more move much multiple must my-custom-directive my-directive myapp myclass mycustomdirective mydirective myfilter mymodule name names necessary need needing needs nesting net nets never new next no not nothing notice novalueeventtriggered now null number numbers numerous object objects odd of often on once one ones only opaque operate operates operating operation option options or order os other others otherwise our out output outputs outside outward over overly override own page parent part particular pass passed past path paths pathway pay people perfect perform performing performs perhaps phpunit picking piece place point portion possible pretend pretty prevents problem problems process produce product projects promise promises propagated properly properties property prove provide providers providing pull purchase purposes put quite rathbury rather read real really reason receiving recommended red redundant refactor refactored refresh regression regularly reject rejected relied relying remember removed rendered repeating require reserved resolve resolved resolving rest restricted result results return returns rewrite rewrites right rootscope rules run running safety same sample say scenario scenarios scope scopes scratches second section see seem self-describing sending sent sentence separate series service services servicespy session sessionstorage set sets setting setup setups seven several shall shifting shorter should simplified simplify simply simulating since situations skipping smoothly so software some somemethod something sometimes source source\ specific spies split spoken stage started states step still string strings structure structured submission submit submitting success successfully such suggest sure surface system tab taken task teardown techniques tell test test\ tested testeffectsofinternalfunction testing testnegativeeffectsofinternalfunction testobject tests text than that that's the their them them! then there there's these thevalue thevalue\ they thing things think third this thisisatest those though thought through throw thus tie time times to tobe toequal together tohavebeencalledwith too touchy traveling tricky triggered trims trivial true truthy try trying turns two type ui uis unavoidable undefined undesirable unit unknownthingsareallowed unless unsuccessful up update updated updates us use used user user's uses using usually utilized valid validvalue value value' values var variable variables variations very view viewpoint vital want was way ways we we'd website well what what's when whenever where whether which while whitespace whole will window windows with without work works world would write writing written wrong wrong? yawn yeah yellow yodel you you'd you'll your yourself yuck ywords zoom zooming
---

These rules extend and override the [general rules][general-rules].


Purposes of Tests
-----------------

1.  Ensure the code works as expected with valid scenarios.

2.  Ensure the code errors as expected with invalid scenarios.

3.  Prove that bugfixes work.

4.  Catch regression issues and problems where interfaces change.

5.  In a way, document the code.

Think of tests as a safety net for acrobats.  You'd rather be perfect and perform your art without ever needing tests, but they are there to help you when a mistake is made.  Tests are a bit better than nets because they help catch problems before you go on stage and perform in front of your audience.


Guidelines
----------

The art of writing tests is quite complicated.  This page only scratches the surface and gives you areas to address.  If there are additional aspects that are missing, feel free to suggest them!

For convenience, the tests assume a Jasmine-based testing system.  It operates with `describe()` blocks that explain what is being tested, `beforeEach()` and `afterEach()` to perform setup and teardown, and `it()` where the actual test lives.  Here's a simplified example.

    describe("MyClass", () => {
        describe(".someMethod()", () => {
            var instance;

            beforeEach(() => {
                instance = new MyClass();
            });
            it("returns true", () => {
                expect(instance.someMethod()).toBe(true);
            });
        });
    });


### Eliminate Duplicated Setup

When the code has two separate actions that it performs then you want to have the tests split into two separate `it()` calls.  These would require the same setup to achieve an identical scenario.  Move that into a `beforeEach()`.  When you have a complicated piece of code that has numerous logical branches, again you will want to split the setup into multiple `beforeEach()` calls, one for each branch.

There's examples later in this document to help explain this process.


### Make it easy to expand

Let's say that your code currently does only one thing.  Perhaps it just trims whitespace.  You'd see no reason to have a `beforeEach()` that would set up some service and then a separate `it()` to test if the whitespace was removed.  You could put all of the setup and the testing together in an `it()`.

It is recommended to not do this.  The `it()` is considered the "test" portion of the code and `beforeEach()` is reserved for setup.  Imagine if there was a bug in this code.  Think about what you would have to do in order to prove this bug was fixed properly.  If the setup was combined with the test, then you'd either have to duplicate the setup in the second test (already you know that's bad) or you'll have to refactor the test to have a `beforeEach()` and two `it()` calls.  Since the latter option is the one we'd like to see, try to make all setup happen in a `beforeEach()` even if there is only one test.  It is much easier to add more tests later with this structure.


### Test Behavior

We want to write tests to not only confirm there are no defects, but also ones that could mimic how the software is intended to be used or how it could work.  By testing behavior, we are shifting our viewpoint to be from the user's point of view instead of being overly concerned with the internals of the software.  In essence, make sure your code performs a specific action to produce the desired result.  Do not guarantee that the code does every specific step in exactly the right order.

When you test behavior, you should be able to completely rewrite the internals of how the job gets done and the tests should all pass.  Depend on inputs and outputs.  Pretend the code is opaque.

Another important thing is to be concerned with errors and how they are propagated back to the calling code.  Tests can help you set up situations where, for example, files do not exist.  Does that reject a Promise, throw an Error, or maybe just return false?  It is an important consideration.

Angular directives that emit events, for instance, should have tests that listen on the parent scope.  Listening on the directive's scope is not correct because those listeners would be triggered by a broadcast as well and we want to ensure the events are traveling the correct direction.


### Every Path, Success And Failure

We aim for 100% code coverage.  There's no real good reason for us to avoid it.  When there is a problem testing code that prevents us from achieving 100% coverage then we should correct the problem instead of skipping tests.

Techniques like dependency injection, mocks, spies, and test doubles all have their place in the testing world.  They help isolate your code to make sure the tests run fast and they perform a specific, consistent action.

Every true and every false branch should be tested.  Every promise should be resolved successfully and also should be rejected.  When considering options, make sure to handle the error scenarios as well as every type of success scenario.

This may seem to contradict the "Test Behavior" section because we must be able to inspect the code to see every possible logical path that would be taken.  There is no conflict - each logical path results in outward behavior that the user might encounter.  Even if the code is later refactored to eliminate many logical paths, the tests should still pass and there would be no need to delete any of the tests that now follow a redundant path.


Sample Test Rewrites
--------------------

This is a sample test for a directive in Angular.  Let's pretend our directive will simply set some property on an isolated scope to the value passed into the directive.  There are many things wrong with this test.

One thing to point out is that Angular tests operate in a mixed environment.  For compatibility, we say that Angular projects do not use arrow functions.

    /*global angular, describe, expect, inject, it, module*/
    describe("myCustomDirective", function () {
        var $scope;

        beforeEach(module("app"));
        it("some property on scope", inject(function ($compile, $rootScope) {
            $scope = $rootScope.$new();
            $compile(angular.element("<div my-custom-directive=\"'test'\"></div>"))($scope);
            $scope.$digest();
            expect($scope.some).toEqual("test");
        });
        it("some property on scope", inject(function ($compile, $rootScope) {
            $scope = $rootScope.$new();
            $scope.test = {
                thisIsATest: true,
                unknownThingsAreAllowed: "Yeah, I guess some are allowed",
                yWords: [
                    "yawn",
                    "yellow",
                    "yodel",
                    "yuck"
                ]
            };
            $compile(angular.element("<div my-custom-directive=\"test\"></div>"))($scope);
            $scope.$digest();
            expect($scope.some).toEqual({
                thisIsATest: true,
                unknownThingsAreAllowed: "Yeah, I guess some are allowed",
                yWords: [
                    "yawn",
                    "yellow",
                    "yodel",
                    "yuck"
                ]
            });
        });
    });

What is wrong?

* The data passed in as $scope.test does not need to have a lot of data.  What the directive accomplishes is merely setting the directive's `$scope.some` to the value itself.

* Since we know the object that `$scope.some` should be, we should use `.toBe()` instead of `.toEqual()`.

* The test names are identical.

Let's rewrite it.

    /*global angular, describe, expect, inject, it, module*/
    describe("myCustomDirective", function () {
        var $scope;

        beforeEach(module("app"));
        it("some property is a string", inject(function ($compile, $rootScope) {
            $scope = $rootScope.$new();
            $compile(angular.element("<div my-custom-directive=\"'test'\"></div>"))($scope);
            $scope.$digest();
            expect($scope.$$childHead.some).toEqual("test");
        });
        it("some property is an object", inject(function ($compile, $rootScope) {
            $scope = $rootScope.$new();
            $scope.test = {};
            $compile(angular.element("<div my-custom-directive=\"test\"></div>"))($scope);
            $scope.$digest();
            expect($scope.$$childHead.some).toBe($scope.test);
        });
    });

What's still wrong?

* We are performing the same setup actions.  Let's move them to a `beforeEach()` so we can add dozens of additional tests.

* The `$scope` variable does not need have such a long lifetime.  It's used independently inside each test.  There's two approaches: move the variable inside the `it()` calls or perform setup on the scope in a `beforeEach()` block.

* The whole `$scope.$$childHead` part is tricky.  Tricky code is bad, especially if Angular changes how the internals work.  We want to limit how many times we use fragile code.  Also, if the directive changes to use multiple scopes or decides to not use an isolated scope, then this bit needs to change for every test.

* Using `inject()` for each test is a bit odd.  Injection is part of the setup for the test and should be restricted to `beforeEach()` calls.

* The test names do not read like a sentence.

Rewrite #2.  Don't be afraid to rewrite code to simplify or to pull out common functionality.

    /*global angular, beforeEach, describe, expect, inject, it, module*/
    describe("myCustomDirective", function () {
        var compile, $parent;

        beforeEach(module("app"));
        beforeEach(inject(function ($compile) {
            $parent = $rootScope.$new();
            compile = function () {
                $compile(angular.element("<div my-custom-directive=\"source\"></div>"))($parent);
                $parent.$digest();
                return $parent.$$childHead;
            };
        }
        it("sets some property to a string", function () {
            $parent.source = "test";
            expect(compile().some).toEqual("test");
        });
        it("sets some property to an object", function () {
            $parent.source = {};
            expect(compile().some).toEqual($parent.source);
        });
    });

There.  Now our variables are set up in the `beforeEach()` and the individual assertions or scenarios are handled by distinct `it()` calls.


Handling Events, Grouping Tests
-------------------------------

Events add a level of difficulty because you need to fire events either above or below the directive and see if they perform the right actions.  You may find it easier to group tests by the initial setup data and then assert that things are operating smoothly.

There's also times that complicated logic will need to get tested.  It is often easier to test every pathway by nesting your logic and setup blocks.

We shall imagine our directive performs a task like this so we can better illustrate the reason for nesting our tests.

* For initial setup
    * If there is a value passed in
        * Call a service (sending the value) that returns a promise
        * When the promise is fulfilled
            * If the promise is fulfilled with an even number
                * Set "even" on scope to true
            * If the promise is fulfilled with an odd number
                * Set "odd" on scope to true
                * Set "number" to be the fulfilled number
            * Otherwise
                * Do nothing
        * When the promise is rejected
            * Set "error" on scope to "promise rejected"
    * If there is no value passed in
        * Emit "no value"
* When receiving "update" event (we intend to be broadcasting)
    * If scope "even" is truthy
        * Do not allow the event through
    * Otherwise
        * Do nothing
* When receiving "dirty" event (we intend to be emitting)
    * If scope "number" is a multiple of seven
        * Do not allow the event through
    * Otherwise
        * Do nothing

That's pretty convoluted.  Really, this code should be refactored to split up the code properly.  It's a very contrived example with way too much complexity.  Thus, it will require some thought when making tests.  Here's the test.  Can you see the things that I am missing?  You'll see a lot of code in the `beforeEach()` blocks everywhere.  This test is carefully structured to allow for future updates and additional tests to be trivial to implement.

    /*global describe, inject*/
    describe("myCustomDirective", function () {
        var compile, $parent, rootScope;

        beforeEach(module("app"));
        beforeEach(inject(function ($compile, $rootScope) {
            rootScope = $rootScope;
            $parent = $rootScope.$new();
            compile = function (html) {
                $compile(angular.element(html))($parent);
                return $parent.$$childHead;
            };
        }));
        describe("initial compile", function () {
            var noValueEventTriggered;

            beforeEach(function () {
                noValueEventTriggered = false;
                allowNoValueEvent = false;
                $parent.on("no value", function () {
                    noValueEventTriggered = true;
                });
            });

            describe("when passed a value", function () {
                var deferred, $scope, serviceSpy;

                beforeEach(inject(function ($provide, $q) {
                    $parent.theValue = {};
                    deferred = $q.defer();
                    serviceSpy = jasmine.createSpy("serviceSpy").andReturn(deferred.promise);
                    $provide.value("aService", serviceSpy);
                    $scope = compile("<div my-custom-directive=\"theValue\"></div>");
                }));
                it("called the service and sent the necessary value", function () {
                    expect(serviceSpy).toHaveBeenCalledWith($parent.theValue);
                    expect(noValueEventTriggered).toBe(false);
                });
                describe("when fulfilled with an even number", function () {
                    beforeEach(function () {
                        deferred.resolve(6);
                        $rootScope.$apply();
                    });
                    it("sets only the 'even' property", function () {
                        expect($scope.even).toBe(true);
                        expect($scope.odd).toBe(undefined);
                        expect($scope.number).toBe(undefined);
                        expect($scope.error).toBe(undefined);
                        expect(noValueEventTriggered).toBe(false);
                    });
                });
                describe("when fulfilled with an odd number", function () {
                    beforeEach(function () {
                        deferred.resolve(3);
                        $rootScope.$apply();
                    });
                    it("sets only the 'odd' and 'number' properties", function () {
                        expect($scope.even).toBe(undefined);
                        expect($scope.odd).toBe(true);
                        expect($scope.number).toBe(3);
                        expect($scope.error).toBe(undefined);
                        expect(noValueEventTriggered).toBe(false);
                    });
                });
                describe("when fulfilled with an object", function () {
                    beforeEach(function () {
                        deferred.resolve({});
                        $rootScope.$apply();
                    });
                    it("sets nothing", function () {
                        expect($scope.even).toBe(undefined);
                        expect($scope.odd).toBe(undefined);
                        expect($scope.number).toBe(undefined);
                        expect($scope.error).toBe(undefined);
                        expect(noValueEventTriggered).toBe(false);
                    });
                });
                describe("when rejected", function () {
                    beforeEach(function () {
                        deferred.reject(new Error("some error"));
                        $rootScope.$apply();
                    });
                    it("sets 'error'", function () {
                        expect($scope.even).toBe(undefined);
                        expect($scope.odd).toBe(undefined);
                        expect($scope.number).toBe(undefined);
                        expect($scope.error).toBe("promise rejected");
                        expect(noValueEventTriggered).toBe(false);
                    });
                });
            });
            describe("no value", function () {
                var eventEmitted;

                // This allows the "no value" event to be emitted and tests it
                beforeEach(function () {
                    allowNoValueEvent = true;
                    eventsEmitted = 0;
                    $parent.on("no value", function () {
                        eventsEmitted += 1;
                    });
                    compile("<div my-custom-directive></div>");
                });
                it("emits 'no value'", function () {
                    expect(eventsEmitted).toBe(1);
                });
            });
        });
        describe("update event", function () {
            var eventPassed, $scope;

            beforeEach(function () {
                $scope = compile("<div my-custom-directive></div>");
                eventPassed = false;
            });
            it("allows the number by default", function () {
                $parent.$broadcast("update");
                expect(eventPassed).toBe(true);
            });
            it("allows the number with even true", function () {
                $scope.even = true;
                $parent.$broadcast("update");
                expect(eventPassed).toBe(true);
            });
            it("disallows the number with even false", function () {
                $scope.even = false;
                $parent.$broadcast("update");
                expect(eventPassed).toBe(false);
            });
        });
        describe("dirty event", function () {
            var $child, eventPassed, $scope;

            beforeEach(function () {
                // Test events coming up from a lower scope
                $scope = compile("<div my-custom-directive></div>");
                $parent.on("dirty", function () {
                    eventPassed = true;
                });
            });
            it("allows the event by default", function () {
                $child.emit("dirty");
                expect(eventPassed).toBe(true);
            });
            it("allows the event when number is 6", function () {
                $scope.number = 6;
                $child.emit("dirty");
                expect(eventPassed).toBe(true);
            });
            it("disallows the event when number is 7", function () {
                $scope.number = 7;
                $child.emit("dirty");
                expect(eventPassed).toBe(false);
            });
        });
    });

That sure is a lengthy example, but carefully notice how anyone could add additional assertions, test cases, alternate setups and different scenarios.  The event testing code is clearly separate from the initialization code.  Promises are used for resolving values.  Events are sent in the correct way through the directive and are tested at the appropriate levels.  Data is flowing through the directive and still you don't tie yourself to any other services or code outside of your directive.


Data Sets
---------

A filter is often tested by providing a series of inputs and asserting the output is correct.  This approach can be utilized whenever you write tests with the same general set of expectations - feed in one value and expect the result to be different.  PHPUnit uses data providers and other frameworks have their variations.

    /*global beforeEach, describe, expect, inject, it, module*/
    describe("myFilter", function () {
        var filter;

        beforeEach(module("myModule"));
        beforeEach(inject(function (myFilter) {
            filter = myFilter;
        }));

        // Define an array of scenarios to test
        [
            {
                input: undefined,
                it: "converts undefined to empty string",
                output: ""
            },
            {
                input: 7,
                it: "converts 7 to "7"",
                output: "7"
            },
            {
                input: "Ian"
                it: "adds Ian's last name",
                output: "Ian Rathbury"
            }
        ].forEach(function (scenario) {
            it(scenario.it, function () {
                expect(myFilter(scenario.input)).toEqual(scenario.output);
            });
        });
    });


Common Tests
------------

Sometimes a directive may call an internal function that performs specific actions.  These actions could be the result of many different inputs.  Instead of repeating the expectations, we pull them into functions.

    /*global angular, beforeEach, describe, expect, inject, it*/
    describe("myDirective", function () {
        var compile, eventData, eventList;

        function testEffectsOfInternalFunction(scope) {
            it("emits 'goAhead'", function () {
                expect(eventList.indexOf("goAhead")).toBe(2);  // Third event
                expect(eventList.lastIndexOf("goAhead")).toBe(2);  // Only once
            });
            it("set validValue to true", function () {
                expect(scope.validValue).toBe(true);
            });
        }

        function testNegativeEffectsOfInternalFunction(scope) {
            it("never emitted 'goAhead'", function () {
                expect(eventList.indexOf("goAhead")).toBe(-1);
            });
            it("deleted or never set validValue", function () {
                expect(scope.validValue).toBe(undefined);
            });
        }

        beforeEach(module("myApp"));
        beforeEach(inject(function ($compile, $rootScope) {
            compile = function (input) {
                var scope;

                scope = $rootScope.$new();
                $compile(angular.element("<div my-directive=\"input\"></div>"))(scope)

                // Directive makes its own isolated scope
                return scope.$$childHead;
            };
        }));
        it("allows numbers", function () {
            var scope;

            scope = compile(7);
            testEffectsOfInternalFunction(scope);
        });
        it("allows objects", function () {
            var scope;

            scope = compile({
                testObject: true
            });
            testEffectsOfInternalFunction(scope);
        });
        it("allows strings", function () {
            var scope;

            scope = compile("a string");
            testEffectsOfInternalFunction(scope);
        });
        it("disallows null", function () {
            var scope;

            scope = compile(null);
            testNegativeEffectsOfInternalFunction(scope);
        });
        it("disallows undefined", function () {
            var scope;

            scope = compile();
            testNegativeEffectsOfInternalFunction(scope);
        });
    });

With the above example, we could combine the data sets with this example to provide even shorter code, but it may be undesirable to do so.  For instance, with this code structure one can assert additional effects happened or mix in several `beforeEach()` calls.  Remember that the goal is maintainable, clean and self-describing code.


Functional Testing
------------------

Functional testing is the art of testing how your website or API works from the eye of a user. Where functional tests differ, is instead of testing a piece of code, they test an entire flow. This could just be from simply logging in to a system to picking a product and simulating the flow all the way to purchase. There are some things which require a little bit of setup or frame of mind then with unit testing.

First, we want to load the page, refresh the browser, or clear any data from memory each time a test is started. This is to make sure we don't carry over anything from one test to another since a browser or system could cache the data. For instance, if some data was set up in a browser `session`, we want to make sure it gets cleared before loading the next test. This can usually be done in an `afterEach()` call using `window.sessionStorage.clear();`.

Try to think what a user would do. Running through the scenario you are setting up and pay attention to what you do. Forms can be a little touchy, as some people will click the button to submit the form, while others will tab to the submit button and hit enter, or just hit enter when in the last field. Try to write tests using different techniques to achieve the same goal, like submitting a form to make sure different ways work. For functional tests without a UI, you would still look at how a user would interact with the system and how they would get data and use it to move through the rest of the system.

Do not test against written or spoken language unless it is something vital or there isn't another way to test, but there should always be another way without relying on content language. This is because the default language or the content could change and then all the tests which relied on this need to be updated. This also applies to API calls where one should be testing against a code, or some other item which would not change regularly.

### Functional Testing of UIs Rendered In Browsers

Whenever possible, test against states of elements and not content. This is to help in case a class or text has changed its name or is not longer included. Sometimes this can't be avoided though. An example of this would be if an unsuccessful form submission turns the button red, but doesn't change whether it is disabled. We would need to test to see if a failure class was added to the button. This can be annoying if the class changes names and thus tests will need to be updated, but in this case it would be unavoidable. Another way to test is would be to see if the message appears to tell the user the submission was a failure.

With browsers, include only browsers which are installed or can run on the a particular Operation System (OS). Internet Explorer should not in the default list of browsers to be tested, but instead it should be checked if the OS is Windows and then include Internet Explorer.

Make sure browsers you are using are set to 100% zoom and your OS is not zooming past 100%. Internet Explorer is fickle in both of these. When writing your functional tests make sure both are set to 100%. If you need to change the OS zoom level, make sure to check the browsers are both set to 100% before trying to test. This can interfere with the ability of using a click method.


{% include links.html %}
