---
title: Shell Cheatsheet
date: 2016-06-03 09:50:09
tags:
    - linux
    - shell
    - cheatsheet
---
+ Checking if string does or not contain other string

**Use '=' or '!='**
```bash
if [[ ${testmystring} = *"c0"* ]];then
    # testmystring does contain c0
fi

if [[ ${testmystring} != *"c0"* ]];then
    # testmystring does not contain c0
fi
```
<!-- more -->