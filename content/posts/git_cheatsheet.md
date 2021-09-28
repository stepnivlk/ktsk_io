+++
title = "Git cheatsheet"
date = 2021-04-12

[taxonomies]
categories = ["programming", "cheatsheet"]
+++

# Break a commit
```sh
git rebase -i <id>^
```
> edit a commit

```sh
git reset HEAD~
```
> add + commit files selectively

```sh
git rebase --continue
```

# Change the author of a commit
```sh
git rebase -i <id>^
```
> edit a commit

```sh
git commit --amend --author="First Last <email@email>" --no-edit
git rebase --continue
```

# Rename a branch
```
git checkout <old name>
```
Rename the local branch:
```
git branch -m <new name>
```
Perform following if pushed to remote:
```
git push origin -u <new name>
git push origin --delete <old name>
```