---
title: MySQL cheatsheet
date: 2017-04-18 10:39:59
tags:
    - linux
    - mysql
---

+ select

1. normal select

```mysql
SELECT column1, column2, ...
FROM table_name; 
```

2. Derived Tables

```mysql
SELECT column1, column2, ...
FROM (subquery) [AS] tbl_name ...
```

+ encoding

```mysql
set CHARACTER SET (encoding)
```
