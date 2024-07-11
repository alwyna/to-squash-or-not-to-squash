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

*this line marks the end of the feature 4*

Seventh PR (feature-4 to develop)

**NO CONFLICT, squashing!**

![alt text](image-11.png)

to be precise:

![alt text](image-10.png)

Eight PR (develop to main)

**NO CONFLICT, and NOT squashing (merge commit)**

![alt text](image-12.png)

Regular merge

![alt text](image-13.png)

*We were expecting a conflict at this point but there is NONE!*

However I suspect a conflict is brewing as there is now a merge commit that is not in develop see:

Notice the most recent commit hash `1846048` is not found in the squashed develop branch, also observe that when develop is merge commited (`feature-1`,`feature-2`), there is *no unique hash, that exists only in main*.

|Main|Develop|
|----|:-----:|
|![alt text](image-14.png)| ![alt text](image-16.png)|

To try and trigger the necessary empty down merge, we are going to squash these changes to develop via. PR and make another PR to main, expecting a conflict. To do that, we are going pull latest from `develop` and create a new `feature-5` branch.

*this line marks the end of the feature 5*