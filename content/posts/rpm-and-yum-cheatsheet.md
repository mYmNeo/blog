---
title: rpm and yum cheatsheet
date: 2016-04-28 10:58:34
tags: 
    - linux
    - rpm
---
+ query the dependency of a package

```bash
rpm -qR <package-name>
```

+ query the dependency of a rpm file

```bash
rpm -qpR <rpm-file>
```

+ query which rpm this file belongs to

```bash
rpm -qif <filename>
```

+ query non-installed rpm file

```bash
rpm -qip <rpm-file>
```

+ setup yum with proxy

append `proxy=<your proxy>` to /etc/yum.conf

```
[main]
proxy=<your proxy>
```

if you don't want proxy in some repository

append `proxy=_none_` to your repo file
