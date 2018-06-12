---
title: Linux Administrator command
date: 2017-05-16 09:53:26
tags:
    - linux
---
# Commands for administrator

+ Disable expiration of a user
>Minimum Password Age to 0
>Maximum Password Age to 99999
>Password Inactive to -1
>Account Expiration Date to -1

```shell
chage -I -1 -m 0 -M 99999 -E -1 <username>
```
<!-- more -->
