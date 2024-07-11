# to-squash-or-not-to-squash

## Motivation

While squashing to develop helps maintain a linear history, it introduces other challenges in the typical git-flow strategy:

* You can't bisect
* When develop is merge commited to main (aka. master), on the next PR you're required to merge down an empty PR
* Which is not an issue, unless the develop branch is also proctected, which adds to non-value-added busy work.

## The experiments

We will create **8 pull-requests (PRs)** total, the first 4 PRs (dev->main->dev-main) will NOT be squashed, the last 4 will be squashed.

We want to test if merge commit to develop avoids an empty down-merge to develop on the second set of PRs.

Additionally we want to show that squashing necessitates an empty down merge.

*This line marks the first commit to feature*

