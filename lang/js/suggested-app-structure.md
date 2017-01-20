Suggested App Structure
=======================

Below is an example application structure. This example uses HTTP as a communication layer but it would work equally well with other communication types.

	├── bin
	├── doc
	├── http
	│   ├── lib
	│   └── route
	├── lib
	└── spec

* `bin` - Executable files. These deal with a Command Line Interface (CLI) as the communication layer. If the executable must use something in another communication layer (for example starting a server for HTTP) add as little from that layer as possible.
* `doc` - All documentation should be under this folder with the exception of a `README.md` which can exist at the root of the project.
* `http` - Everything having to do specifically with HTTP should go under this folder. That includes anything that uses the request, the response or the session.
    * `lib` - The core functionality for dealiing with HTTP. In theory, modules here could be reused with other HTTP interfaces.
    * `route` - Route handlers. These are not reusable in another HTTP interface unless you were building the same HTTP interface.
* `lib` - This folder contains all core functionality that doesn't touch a communication layer (for example HTTP). Most of your code should be found here.
* `spec` - Contains all tests. This should mirror the repository (with the exception of the `spec` folder).

All folder names should be singular.

Subfolders
----------

Subfolders should group by functionality instead of by a certain type. For example, you wouldn't want a `manager` folder where you would put a `registration-manager.js` and an `account-search-manager.js` but you might want a `registration` folder where you would place a `manager.js` and a `mapper.js`.
