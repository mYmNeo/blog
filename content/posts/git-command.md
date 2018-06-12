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
+ hook
>
Installing a Hook

To enable a hook script, put a file in the hooks subdirectory of your .git directory that is named appropriately (without any extension) and is executable. From that point forward, it should be called. We’ll cover most of the major hook filenames here.

Committing-Workflow Hooks
The first four hooks have to do with the committing process.

The pre-commit hook is run first, before you even type in a commit message. It’s used to inspect the snapshot that’s about to be committed, to see if you’ve forgotten something, to make sure tests run, or to examine whatever you need to inspect in the code. Exiting non-zero from this hook aborts the commit, although you can bypass it with git commit --no-verify. You can do things like check for code style (run lint or something equivalent), check for trailing whitespace (the default hook does exactly this), or check for appropriate documentation on new methods.

The prepare-commit-msg hook is run before the commit message editor is fired up but after the default message is created. It lets you edit the default message before the commit author sees it. This hook takes a few parameters: the path to the file that holds the commit message so far, the type of commit, and the commit SHA-1 if this is an amended commit. This hook generally isn’t useful for normal commits; rather, it’s good for commits where the default message is auto-generated, such as templated commit messages, merge commits, squashed commits, and amended commits. You may use it in conjunction with a commit template to programmatically insert information.

The commit-msg hook takes one parameter, which again is the path to a temporary file that contains the commit message written by the developer. If this script exits non-zero, Git aborts the commit process, so you can use it to validate your project state or commit message before allowing a commit to go through. In the last section of this chapter, We’ll demonstrate using this hook to check that your commit message is conformant to a required pattern.

After the entire commit process is completed, the post-commit hook runs. It doesn’t take any parameters, but you can easily get the last commit by running git log -1 HEAD. Generally, this script is used for notification or something similar.

Email Workflow Hooks
You can set up three client-side hooks for an email-based workflow. They’re all invoked by the git am command, so if you aren’t using that command in your workflow, you can safely skip to the next section. If you’re taking patches over email prepared by git format-patch, then some of these may be helpful to you.

The first hook that is run is applypatch-msg. It takes a single argument: the name of the temporary file that contains the proposed commit message. Git aborts the patch if this script exits non-zero. You can use this to make sure a commit message is properly formatted, or to normalize the message by having the script edit it in place.

The next hook to run when applying patches via git am is pre-applypatch. Somewhat confusingly, it is run after the patch is applied but before a commit is made, so you can use it to inspect the snapshot before making the commit. You can run tests or otherwise inspect the working tree with this script. If something is missing or the tests don’t pass, exiting non-zero aborts the git am script without committing the patch.

The last hook to run during a git am operation is post-applypatch, which runs after the commit is made. You can use it to notify a group or the author of the patch you pulled in that you’ve done so. You can’t stop the patching process with this script.

Other Client Hooks
The pre-rebase hook runs before you rebase anything and can halt the process by exiting non-zero. You can use this hook to disallow rebasing any commits that have already been pushed. The example pre-rebase hook that Git installs does this, although it makes some assumptions that may not match with your workflow.

The post-rewrite hook is run by commands that replace commits, such as git commit --amend and git rebase (though not by git filter-branch). Its single argument is which command triggered the rewrite, and it receives a list of rewrites on stdin. This hook has many of the same uses as the post-checkout and post-merge hooks.

After you run a successful git checkout, the post-checkout hook runs; you can use it to set up your working directory properly for your project environment. This may mean moving in large binary files that you don’t want source controlled, auto-generating documentation, or something along those lines.

The post-merge hook runs after a successful merge command. You can use it to restore data in the working tree that Git can’t track, such as permissions data. This hook can likewise validate the presence of files external to Git control that you may want copied in when the working tree changes.

The pre-push hook runs during git push, after the remote refs have been updated but before any objects have been transferred. It receives the name and location of the remote as parameters, and a list of to-be-updated refs through stdin. You can use it to validate a set of ref updates before a push occurs (a non-zero exit code will abort the push).

Git occasionally does garbage collection as part of its normal operation, by invoking git gc --auto. The pre-auto-gc hook is invoked just before the garbage collection takes place, and can be used to notify you that this is happening, or to abort the collection if now isn’t a good time.
>
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