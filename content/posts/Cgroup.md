Cgroup

---
title: cgroup controlle memo
date: 2020-01-14 11:48:34
tags: 
    - linux
    - cgroup
    - grub
---

- Disable cgroup v1 in grub

For Ubuntu:

vim /etc/default/grub

```
GRUB_CMDLINE_LINUX="cgroup_no_v1=all"
```