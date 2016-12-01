---
title: Style Guide Goals
pageid: goals
summary: A style guide does more than enforce arbitrary rules.  Its mandates are based on removing problems.
keywords: 1 100% a able about accumulate active added adding addition addressed adjust advanced advantage after aim all almost also alternative always amount an and anotherexample any anyone application approach aptly are areas arguments as assignments async at auditing automated automatically avoid bar base based be because become been before behaves being benefits better between big bits break bug but by call calls can capital cause chained change changes check checker circles class classified clean cleaner clever code codebase coding communicated communication complaint complex complexity confirm conflicts consider considered consistency consistent consistently control correctly could coverage crop cyclomatic data deal debt debugged debugging deeper define dependency destroys detect developer developers development did do documentation does doesn't done don't dreads dream due during each early easier easily either eliminate emails employed end end-to-end enforced ensure ensures entire especially essential even ever everyone everything everywhere example exist exists expected experience experienced far fast faster feature feel few files find finding following for found frustration function functional functionality functions fundamentals future gaining gains getnameasync goal goals going grows guiding has hate have having help helps high hints hooked how huge ideas if i'm immediately improve improvement in included indentation indication information injection in-line inputs inspect instance instead integrate integration intend interest interface internals into investment is issues it it's itself javascript job just keep know known knows language larger later leading legacy less let letter letting levels libraries library like line lines lint listing lofty long look looks maintain maintainable make mangled manually many means merge mind minify minimized minor mocks module modules months more most much multiple mysterious named near necessary necessity need needed needs never new no not notice nuances object objective obscure observe obvious of on one only or other our out outputs overlook partially particular parts passed pattern patterns people perfect perform perhaps person philosophy picky places plainly pleasure plus possibly post-increment practice pre-increment problem problems produced programmer programmers progresses project projects promise provide purpose quality raise raised rarely read realize really real-world refactoring reference referencing rely remember repeated requiring return review reviewing reworked right routines rule same save saying scenario scenarios see seemingly sees segment separate share should simulate skimmed so software solution solve some someone something somethingspecial sometimes somewhere sooner spaces spies split splitting standard standards starts statement steps straightforward strive structured style subtle suite support switching syntax system systems tabs take taken teach team technical techniques tell test testable tested testing tests than that that's the their them then there's these they things this though time to too tools topic train trick tricks tricky trivial truly trying twice type ugly understand understanding unforeseen unit unless unravel up update us use used uses using usually variable variables very violations was way ways we weeks well when where which while who whole why wiki will with wonderful work works would writing written wrong yaml you you'd your you've
---

Maintainable Code
-----------------

When a developer looks at projects, the software will be immediately classified as either "legacy" or "active".  Everyone dreads legacy code because even minor, seemingly trivial changes can cause huge and unforeseen issues.  Legacy code also rarely sees anyone refactoring modules to improve how they work or to change their interface to be more in-line with a better practice.  Our goal is to raise the bar so high that our project will be a pleasure to update and developers will have many ways to adjust our code in the future.  It's a lofty goal, but steps can be taken to help realize our dream.


### Clean and Straightforward

One big complaint about software is that the developers need months to understand each obscure trick that the application uses.  We aim for consistency in our approach.  Code that is able to be debugged should be consistently produced, which is why one should *code plainly* and use obvious techniques instead of subtle nuances.  Avoid tricky parts and clever bits.  Don't manually minify code, let software do that for you as needed.  For example, it's far better to use an `if` statement than `||`.  This has the added advantage of being able to easily see how your cyclomatic complexity grows in functions.

Following a coding standard can provide hints on how to use functions and variables.  For instance, you could be writing JavaScript and use the function `getNameAsync()` and you'd know it would return a Promise because all functions that return a Promise should end in `Async`.  The variable `SomethingSpecial` is a class due to the leading capital letter, where as `anotherExample` is not a class (though it could be either a base data type or an instance).

Documentation helps unravel mysterious parts.  Even after only a few weeks, developers do not remember the tricks they employed to solve a problem.  Adding documentation for these complex areas is a necessity and can help you or anyone who has to maintain the code in the future.

When the syntax starts to look ugly, take that as an indication that there's too much going on or that the code needs to be reworked.  When you feel like listing variables on multiple lines or splitting up your chained calls, perhaps it is better to consider an alternative.  Too many arguments to one function?  The functionality could be split into separate routines or you could define an object that helps control the data being passed.  Very long chained calls?  Repeated assignments can help split the line up and make it easier to read for the less experienced people on the team.


### Consistent Writing Style

When you always deal with the same writing style, you train your mind to observe patterns and will notice problems sooner.  Code can be skimmed faster and it will provide a deeper understanding of the purpose of the code segment when it is structured the same everywhere.  Plus, using a writing style that is enforced by tools can help detect problems early.

This helps out in other ways.  For instance, merge conflicts are minimized because everyone uses the same type and amount of indentation.  YAML files are not mangled when switching between tabs or spaces.  The pattern of writing can make development of auditing tools easier.

The consistent writing style is usually enforced with a lint checker.  Some people really hate these tools because of how picky they are with code.  Each type of check is based on real-world experience and problems found during debugging.  Letting it find all of these problems in our code helps us become better programmers while also finding places where problems could crop out later.  Using these tools during development means we can find problems before they even exist.  I'm not saying that you would automatically do it wrong if you use `++`, but it is more tricky than using `+= 1`.  How so?  Well, did you intend to do post-increment or pre-increment?  Does the language truly support that, or does it simulate it in some scenarios?


Tested Correctly
----------------

We rely on tests to confirm that our code works and that we don't ever experience a bug twice.  They define how our code should be used and can be used as a reference when trying to see how things work.  Tests tell us when we are done writing a feature and confirm no future changes break our code.


### Near 100% Code Coverage

We use module systems to perform dependency injection for us.  With mocks and the use of spies, all of our code should be able to be tested.  There's almost no scenario where code would not be able to be tested.


### Test How Code Behaves

Tests are written to simulate expected inputs and outputs of the test.  We simulate inputs and check the outputs.  Do not inspect the internals of an object unless it is necessary.


### Levels of Tests

We strive to have fast tests that ensure the libraries do their job correctly.  They could be considered unit tests as long as you define *unit* as *the library*.  Other people call them integration tests, though the library itself doesn't integrate with any other library for these tests.

In addition, having end-to-end tests (also known as functional tests or system tests in some circles) ensures that you've hooked up the libraries correctly.  These also should be automated and included in the test suite.

There's a whole [topic about testing][topic-tests] for more information.


Become Better Programmers
-------------------------

No programmer knows everything.  Even the most advanced programmers sometimes overlook ideas.  New things crop up all the time.  One of our goals with having these high standards is to make better programmers out of everyone.  The entire team benefits.


### Share Ideas

That's why this documentation exists.  It is to share ideas with you.  In particular, these ideas are just to save time and frustration with partially communicated emails or referencing a wiki somewhere.  Communication with your other developers, especially about the philosophy or the fundamentals of the codebase, is *essential* to gaining understanding.


### Improve the Software

It's never perfect.  When you see something that was not done right and it should have been done in a cleaner or more testable way, then that should be raised and possibly addressed.  Letting technical debt accumulate destroys projects.  It's aptly named "technical debt" because it gains interest as time progresses, requiring a larger and larger investment later to eliminate the debt.


### Code Review

The objective is to have high quality code.  When reviewing code, look for rule violations as well as areas of improvement.  This is a wonderful time to teach someone by guiding them to a better solution.  Keep in mind that you are reviewing the code, not the person.

{% include links.html %}
