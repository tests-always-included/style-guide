---
title: Git Commits, Branches, Tags
pageid: topic-git
---

These rules extend and override the [general rules][general-rules].


Branching and Tagging
---------------------

Use a [git-flow](http://nvie.com/posts/a-successful-git-branching-model/) branching model.  `master` is the current, live production system.  `develop` is a well-tested version that is aleays ready for immediate release.  There will be other feature branches forked from `develop` to fix bugs or add features.  A critical bug would be fixed by forking `master`, fixing the bug, merging back to `master` (and redeploying), then merging `master` into `develop`.

The feature branches and bugfix branches are expected to be maintained or removed.

When releasing, a new version will be tagged.  We use [semantic versioning](http://semver.org/).  Environments higher than "development" will always be based off a tagged release.  When publishing software to repositories, such as `npm`, the published software will get tagged.  Tags need to get pushed to the central repository.

Branch names will use lowercase letters, numbers and hyphens.  The name should describe the one feature that is being added.  If dealing with a bug related to a numbered issue, the branch name should reflect the issue, eg `issue-1337`.


{% include links.html %}
