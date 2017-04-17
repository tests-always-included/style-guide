---
title: Style Guide for Angular
pageid: lang-js/angular
keywords: #tooling $routeprovider $scope $scope, 'sessions'; 1 2 [angular [assigning [bindable [controlleras [eslint [eslint] [iife] [iife]s [js [jscs] `$inject` `$scope` `activate` `use `vm` a a1 above access accessible activate activation adhere ae again all also an and angular angular-styleguide annotating app application are as assigne assigned assigning at avoided away bad basically be because before being below bindable bindcontroller: blob but by called callout calls can capabilities case clean code com compile compiled component config contained controller controller, controller: controlleras controlleras: controllercontroller controllers controllers] customizability decided declaring defined dependencies dependency developing directive directives div do do, document don't done easier element employ every everything example except factories factory file file, for format formatted function function1 function1, function2 function3 functionality functionality, functions game games gamescontroller generate get github gives global gotosession gotosession; guide guide] have hint] how html https: identify if iife in included information inject injection instead into invoking is it johnpapa js jscs jshint just keeps like liked lines make makes manual manually master md#assigning-controllers md#bindable-members-up-top md#controlleras-with-vm md#js-hint members members] memory merged methods minified module more need needing needs ng-controller no not nothing of on one only or order outside path placement practice presented primary promises properties provides put readme refer refresh refresh; regards remove require resolve resolving restrict: return returning route rules same scope scope: search search; section section] sections service services sessions sessionscontroller should shouldn't since some sources stated strict strict` structure style superfluous supersedes supplies sure tempate template template: templateurl: the them, there they this those title to top topics true, truncated unless unneeded up us use using var variable variable1 variable1, variable2 variable2; variables view, vm vm] want waste way we we've what when which will with within without wrap your
---

For this guide adhere to the [Angular 2 Style Guide] or the [Angular 1 Style Guide] unless stated below which supersedes those rules.

Topics for this document are in the same order as they are in the [Angular 1 Style Guide].


IIFE
----

We don't require the use of [IIFE] for every component. We compile all code into one file, remove all the `use strict` lines and put a `use strict` at the top of the minified file when compiled.

We can get away with this because we do not employ the use of global variables within the Angular scope. It is bad practice to use them, and will be avoided when developing an Angular application.

Generate your code without using superfluous [IIFE]s.

    // controller.js
    "use strict";

    angular.module("module").controller("SessionsController", function ($scope, dependency) {
        var variable1, variable2;

        function gotoSession() {
          /* */
        }

        function refresh() {
          /* */
        }

        function search() {
          /* */
        }

        $scope.gotoSession = gotoSession;
        $scope.refresh = refresh;
        $scope.search = search;
        variable1 = [];
        variable2 = 'Sessions';
    });

If needing an activation function as can be the case when invoking a controller for a directive wrap everything within an `activate` function.

    // controller.js
    "use strict";

    angular.module("module").controller("SessionsController", function ($scope, dependency) {
        this.activate = () => {
            function gotoSession() {
              /* */
            }

            function refresh() {
              /* */
            }

            function search() {
              /* */
            }

            $scope.gotoSession = gotoSession;
            $scope.refresh = refresh;
            $scope.search = search;
            $scope.sessions = [];
            $scope.title = 'Sessions';
        };
    });


Controllers
-----------


### controllerAs with vm

Supersedes the topics presented in the [controllerAs with vm](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#controlleras-with-vm) section.

We don't require the use of using a variable like `vm` within a controller, properties and methods can be assigned to `$scope` when they need to. Just make sure to only assigne to `$scope` what needs to be accessible.


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

Services and Factories are formatted the same way and only return the functions outside sources should have access to.

    // factory.js
    "use strict";

    angular.module("app").factory("service", () => {
        function function1 () {
            /* */
        }

        function function2 () {
            return function3();
        }

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

### Manually Identify Dependencies

The dependencies shouldn't use the `$inject` since we can inject the dependencies in the primary function when declaring the component.

    // controller.js
    "use strict";

    angular.module("module").controller("SessionsController", function ($scope, dependency) {
    // truncated to callout top section


Resolving Promises
------------------

### Route Resolve Promises

This is unneeded to do, since the controller should be only included in the directive or element. This again keeps the code clean and functionality contained in the module.


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
