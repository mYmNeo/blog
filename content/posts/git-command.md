---
title: git command
date: 2016-04-28 17:43:31
tags: 
    - git
---
+ branch
```bash
git checkout -b <branch name> # checkout with <branch name>
git push origin <branch name> # push changes to remote named 'origin' with <branch name>
git push origin :<branch name> # delete remote named 'origin' <branch name>
```
+ commit
```bash
git rebase -i <commit lists> # rebase <commit lists> with interactive mode, it can re-order commits
git reset --hard <commit id> # Resets the index and working tree. Any changes to tracked files in the working tree since <commit> are discarded.
git reset --mixed <commit id> # Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.
git show <commit id> # show <commit id> content
```

+ patch
```bash
git format-patch -1 <commit id> # generate patch related to <commit id>
git format-path HEAD~n # generate last n commits patches
git am <patch name> # apply <patch name>
git apply --reject <patch name> # apply the files without conflicts in patch, leave conflict files with tags
```
+ repository
```bash
git fetch <repository>
git checkout master
git rebase <repository>/master
git push -f origin master
# all the above are used to update a forked repository
```
+ history
```bash
git log -p <filename> # view the change history of <filename>
```
+ archive
```bash
git archive <branch name> --prefix=<prefix> --format=<zip,tar> -o <filename>
```
+ recover delete commit
    1. back up your entire directory, including the .git directory.
    1. You can use `git fsck --lost-found` to obtain the ID of the lost commits.
    1. rebase or merge onto the lost commit.
+ get current branch name
```bash
git rev-parse --abbrev-ref HEAD
```
+ clean remote branch
```bash
git remote prune <remote repository>
```