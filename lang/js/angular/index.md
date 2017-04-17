---
title: Style Guide for Angular
pageid: angular
keywords: #tooling $inject $routeprovider $scope 'sessions' 1 2 @param @property @return @typedef a a1 above accessible activate activation adhere ae again all also an and angular angular-styleguide angular~$scope angular~directive annotating app application are as assign assigned assigning at bad basically be because before being below bindable bindcontroller blob build but by called callout calls can capabilities case clean code collection com compile component config contained controller controller's controlleras controllercontroller controllers customizability decided declaring defined dependencies dependency describe developing directive directive's directives div document don't done duplicate easier element eliminated eslint every everything example except explicit factories factory factory's file files finally for forbidden format formatted from function function's function1 function2 function3 functionality functions game games gamescontroller generate github gives global goal good gotosession guide have having hint how html https identify if iife in included information inject injection inserted inside instead into invoking is it johnpapa js jscs jshint just keeps like liked lines make makes manual manually master md#assigning-controllers md#bindable-members-up-top md#controlleras-with-vm md#js-hint members memory merged methods minified module module~dependency module~factory more nearly need needing needs ng-controller no nothing object obvious of on one only or order our outside path placement possible practice presented primary procedure processes promises properties provides purpose put readme refer refresh regards removing repeat require resolve resolving restrict return returning route routes rules s same scope search section sections service services sessionscontroller should shouldn't since some stated static strict structure style superfluous supersedes supplies sure tempate template templateurl that the their them there they thing things this those to top topics true truncated type unless unnecessary up us use used using var variable variable1 variable2 variables view visible vm want waste way we we've what when which will with within without wrap
---

For this guide, adhere to the [Angular 2 Style Guide] or the [Angular 1 Style Guide] unless stated below, which supersedes those rules.

Topics for this document are in the same order as they are in the [Angular 1 Style Guide].


IIFE
----

[IIFE] for every component.  A build procedure should compile all files into one file, duplicate `"use strict;"` lines are eliminated one is inserted at the top and finally the file is minified. This is possible because no global variables are used within the Angular scope. It is bad practice to use them and nearly forbidden when developing an Angular application.

Generate code without using superfluous [IIFE]s.

    // controller.js
    "use strict";


    /**
     * Describe controller's purpose.
     *
     * @param {module~dependency} dependency
     */
    angular.module("module").controller("SessionsController", (dependency) => {
        var variable1, variable2;


        /**
         * Describe function's purpose.
         */
        function gotoSession() {
          /* */
        }


        /**
         * Describe function's purpose.
         */
        function refresh() {
          /* */
        }


        /**
         * Describe function's purpose.
         */
        function search() {
          /* */
        }

        this.gotoSession = gotoSession;
        this.refresh = refresh;
        this.search = search;
        variable1 = [];
        variable2 = 'Sessions';
    });

If needing an activation function as can be the case when invoking a controller for a directive, wrap everything within an `activate` function.

    // controller.js
    "use strict";


    /**
     * Describe controller's purpose.
     *
     * @param {module~dependency} dependency
     */
    angular.module("module").controller("SessionsController", (dependency) => {
        this.activate = () => {
            /**
             * Describe function's purpose.
             */
            function gotoSession() {
              /* */
            }


            /**
             * Describe function's purpose.
             */
            function refresh() {
              /* */
            }


            /**
             * Describe function's purpose.
             */
            function search() {
              /* */
            }

            this.gotoSession = gotoSession;
            this.refresh = refresh;
            this.search = search;
            variable1 = [];
            variable2 = 'Sessions';
        };
    });


Controllers
-----------

Our goal is to make things more explicit and obvious.


### controllerAs with vm

Supersedes the topics presented in the [controllerAs with vm](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#controlleras-with-vm) section.

We don't require the use of using a variable like `vm` within a controller, properties and methods can be assigned to `this` when they need to. Just make sure to only assign to `this` what needs to be accessible.


### Bindable Members Up Top

Supersedes some topics presented in the [Bindable Members](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#bindable-members-up-top) section.

We don't want all the bindable members at the top if it calls a function as the called functions shouldn't be called before they are defined. Refer above for example on how to structure code in regards to placement of methods and properties.


### Assigning Controllers

Supersedes some topics presented in the [Assigning Controllers](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#assigning-controllers) section.

If a controller is to be assigned within a view, it should be put into the template. This makes it easier and everything is contained within the template and module.

    // config.js
    "use strict";

    function config($routeProvider) {
        $routeProvider
            .when("/games", {
                templateUrl: "app/game/games.html"
            });
    }

    angular.module("app").config(config);

Template:

    <!-- games.html -->
    <div ng-controller="GamesController as games">
    </div>


Services and Factories
----------------------

Services and Factories are formatted the same way and only return the collection of functions that should be visible from outside.

    // factory.js
    /**
     * Describe the type.
     *
     * @typedef {Object} module~factory
     * @property {Function} function1
     * @property {Function} function2
     */
    "use strict";

    /**
     * Describe factory's purpose.
     *
     * @return {module~factory}
     */
    angular.module("app").factory("service", () => {
        /**
         * Describe function's purpose.
         */
        function function1 () {
            /* */
        }


        /**
         * Describe function's purpose.
         */
        function function2 () {
            return function3();
        }


        /**
         * Describe function's purpose.
         */
        function function3 () {
            /* */
        }

        return {
            function1,
            function2
        }
    });


Directives
----------

There is no need to format the directive by returning a variable. This is a waste of memory and lines as there is nothing being done with the variable except to return it.

    // directive.js
    "use strict";

    /**
     * Describe the directive's purpose.
     *
     * @return {angular~directive}
     */
    function directive () {
        return {
            bindController: true,
            controller: "ControllerController",
            controllerAs: "vm",
            restrict: "AE",
            scope: {
                // scope properties
            },
            templateUrl: "path/to/tempate.html"
        }

        angular.module("module").directive("directive", directive);
    }


Manual Annotating for Dependency Injection
------------------------------------------

We are removing manual processes and repeat code.


### Manually Identify Dependencies

Dependencies shouldn't use `$inject` since we can inject the dependencies in the primary function when declaring the component.

    // controller.js
    "use strict";

    /**
     * Describe the controller's purpose.
     *
     * @param {angular~$scope} $scope
     * @param {module~dependency} dependency
     */
    angular.module("module").controller("SessionsController", ($scope, dependency) => {
    // truncated to callout top section


Resolving Promises
------------------

Having promises inside controllers is a good thing, but we don't want to have them in routes, as controllers and their functionality will be defined in static HTML or within a directive.


### Route Resolve Promises

This is unnecessary, since the controller should be only included in the directive or element. This again keeps the code clean and functionality contained in the module.


JSHint and JSCS
---------------

Supersedes some topics presented in the [JS Hint](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#js-hint) and [JSCS] sections.

We've decided to use [ESLint] instead of [JS Hint]. This provides us basically the same functionality, but we liked the customizability more. Refer to the [ESLint Style Guide Section](./#tooling) for more information on using [ESLint]. [ESLint] also gives the capabilities of what [JSCS] supplies since they have merged.


[Angular 1 Style Guide]: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md
[Angular 2 Style Guide]: https://angular.io/docs/ts/latest/guide/style-guide.html
[ESLint]: http://eslint.org
[IIFE]: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#iife
[JSCS]: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#jscs
[JS Hint]: http://jshint.com/
