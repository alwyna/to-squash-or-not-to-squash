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

### NO Squash

#### Observations

##### First Release

First PR (feature-1 to develop)

**NO CONFLICT**
![alt text](image.png)

Second PR (develop to main)

**NO CONFLICT**
![alt text](image-1.png)

##### Second Release

We branched off develop that had the merge commit from `feature-1`

> ~/workspace/to-squash-or-not-to-squash$ git checkout -b feature-2
Switched to a new branch 'feature-2'

*This line marks the commit to feature-2*

#### Observations

Third PR (feature-2 to develop)

**NO CONFLICT**
![alt text](image-2.png)

Fourth PR (develop to main) **!MOMENT OF TRUTH!**

**NO CONFLICT**

Merge committing from feature-> develop -> main does **NOT** cause the empty down-merge issue.
![alt text](image-3.png)

## SQUASHING

To show that squashing results in merge conflicts with no file on the subsequent merge to main.

We branched off develop that had the merge commit from `feature-2`

> ~/workspace/to-squash-or-not-to-squash$ git checkout -b feature-3
Switched to a new branch 'feature-3'

*This line marks the commit to feature-3*

Fifth PR (feature-3 to develop)

**NO CONFLICT, squashing!**

![alt text](image-4.png)

![alt text](image-5.png)

Sixth PR (develop to main)

**NO CONFLICT, and NOT squashing (merge commit)**

![alt text](image-6.png)

to be precise:

![alt text](image-7.png)

