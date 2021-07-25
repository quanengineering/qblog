---
layout: single
title: "Git cheat sheet"
date: 2021-07-25
last_modified_at: 2021-07-25
tags:
  - Git
lang: en
---

Commonly used Git commands for easy reference.

## Remove the last commit but still preserve changes

```
git reset --soft HEAD~
```

## Take all the changes that were committed on one branch and replay them on a different branch

BEWARE: Do **NOT** rebase public history

E.g. rebase the `feature` branch onto the `main` branch using the following commands:

```
git checkout feature
git rebase main
```

`rebase` gets a much cleaner project history than `merge` because it eliminates the unnecessary merge commits required by git merge.

References: [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

## Combining multiple commits

[Git rebase interactive](https://stackoverflow.com/a/21278908/5827002) can be used to squash multiple commits.
