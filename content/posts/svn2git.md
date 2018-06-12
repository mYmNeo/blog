---
title: SVN and Git migration
date: 2016-07-15 10:05:33
tags:
    - linux
    - svn
    - git
---
# Import svn project into your git project
```shell
git config --add svn-remote.<branch name>.url <svn repository url>
git config --add svn-remote.<branch name>.fetch :refs/remotes/<branch name>
git svn fetch <branch name> [-r<rev>]
```
# Export and import SVN repository
```shell
svnrdump dump [-r<rev>] <svn repostory url> > <dump file>
svnadmin load --force-uuid <directory> < <dump file>
```
<!-- more -->