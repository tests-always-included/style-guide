---
title: Git Commits, Branches, Tags
pageid: topic-git
keywords: a a-successful-git-branching-model add added always and apply are as at back base based be being branch branches branching bug bugfix bugs by central com critical current dealing describe develop development directories eg end environments expected extend feature features file files fix fixed fixing folder for forked forking from general general-rules get git-flow gitignore higher http hyphens if ignoring immediate in into is issue issue-1337 leading letters live lowercase maintained master means merging model name names need new npm numbered numbers nvie of off one only or org other our override posts production published publishing pushed ready redeploying reflect related release releasing remember removed repositories repository root rule rules semantic semver should software something such system tagged tagging tags than that the then there these to txt use version versioning want we well-tested when will with would you
---

These rules extend and override the [general rules][general-rules].


Ignoring Files
--------------

Use our [.gitignore](gitignore.txt) file as a base.  Remember that directories should end in `/` if you only want to apply the rule to a folder and a leading `/` means you only want something at the root of the repository.


Branching and Tagging
---------------------

Use a [git-flow](http://nvie.com/posts/a-successful-git-branching-model/) branching model.  `master` is the current, live production system.  `develop` is a well-tested version that is always ready for immediate release.  There will be other feature branches forked from `develop` to fix bugs or add features.  A critical bug would be fixed by forking `master`, fixing the bug, merging back to `master` (and redeploying), then merging `master` into `develop`.

The feature branches and bugfix branches are expected to be maintained or removed.

When releasing, a new version will be tagged.  We use [semantic versioning](http://semver.org/).  Environments higher than "development" will always be based off a tagged release.  When publishing software to repositories, such as `npm`, the published software will get tagged.  Tags need to get pushed to the central repository.

Branch names will use lowercase letters, numbers and hyphens.  The name should describe the one feature that is being added.  If dealing with a bug related to a numbered issue, the branch name should reflect the issue, eg `issue-1337`.


{% include links.html %}
