---
title: rpm command
date: 2016-04-28 10:58:34
tags: 
    - linux
    - rpm
---
+ query the dependency of a package
```bash
rpm -qR <package-name>
```
<!-- more -->
+ query the dependency of a rpm file
```bash
rpm -qpR <rpm-file>
```
+ query which rpm this file belongs to
```bash
rpm -qif <filename>
```