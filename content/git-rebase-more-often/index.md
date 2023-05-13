---
title: "git-rebase more often"
description: "I cannot stress this enough. I wish GitHub would offer a default git rebase setting as part of its pull requests."
date: "2018-01-02T10:24:44.303Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/git-rebase-more-often-98bd00ab9e5e
redirect_from:
  - /git-rebase-more-often-98bd00ab9e5e
---

I cannot stress this enough. I wish [GitHub](https://github.com) would offer a default git rebase setting as part of its pull requests.

Here’s a workflow which I’m sure is common:

-   `master`— this is the develop branch from which all release tags are created. When we’re ready to release, we create a release branch, update versions, tag it.
-   `release-XXX` — unimportant to describe. It’s the release. It matters when we’ve got a production bug but I’m not interested in exceptional cases here.
-   feature branches — when developing some feature (or fixing a bug) we create a feature branch off `master` and work on it.

Since we release often the feature branches often lag behind master and must be kept up-to-date. Here the most common practice I’ve seen is to merge master into the feature branch creating a merge commit in the process. This is ugly. The practice should be to always rebase the feature branch against master. Not only does this make the `gitk` graphs look better and easier to read but it also makes reading `git-log` and `git-diff` outputs easier to read.

#### Case in point

**aka what prompted this blog post**

We had two features being developed. Let’s call them feature\_foo and feature\_bar. Now, feature\_foo depends on some features in feature\_bar but neither are ready to be merged into master. At some point, feature\_foo was updated with feature\_bar _and_ master and the history looked like below.

```
 A-B-C-D-E-F-G-H-I-J-K     feature_foo
            /   /               
   N-O-P-Q-R   /           feature_bar
        /     /                 
       M-----’             master
```

In above, `HEAD` is at `K`, which is also feature\_foo; `master` was merged into it at `I` and, on `feature_bar` at `Q` too.

Question: how do I compare changes in `feature_foo` but ignore changes from `feature_bar`?

Answer: `git log HEAD ^master ^feature_bar`

This is so ugly that it makes me want to tear my hair out. (It’s simple here and I know there’s `git log --right-only` but it’s annoying and unnecessary. This isn’t about what is and isn’t possible but about what’s convenient for most cases.)

Question 2: what if I want to see just the commits from E to K, but ignore N, O, P, Q, R, G, and I?

Answer: `git log E K ^master ^feature_bar --no-merges`

Now suppose `master` and `feature_bar` have been merged into `feature_foo` more than once. Perhaps even `feature_quux` was merged in at some point. If I have to keep track of all these extraneous changes just see what changes were made it’s not a comfortable workflow.

#### Alternative

Never merge master into your feature branches. Always, always rebase master to your feature branch. There’s never a commit of the form `merge master into feature_XXX`. Now `git log feature_XXX..master` is always empty (post rebase), `gitk` is simpler, and `git log master..feature_XXX` shows all and only the commits required to implement `feature_XXX`.

I’m ambivalent about whether other feature branches should be merged into ongoing feature branches or not. Perhaps when ready for merge into master it must be rebased to be flat. I don’t have any strong opinions at this time.

The biggest advantage to this scheme is that it leads to good looking and easy to read histories. Realistically, nobody really cares how many times a feature branch was synced with master or other branches. The things that matter are (a) how the feature was implemented and (b) when it found its way into master.

Code history, to be at all usable, must be presented in a careful manner just as code itself is. All criteria that apply to writing good code also apply to how the history of a project is presented.
