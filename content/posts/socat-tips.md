---
title: socat tips
date: 2017-08-24 15:44:50
tags:
    - linux
---
# Tips for socat

1. listen tcp port and transport data to unix socket
```bash
socat TCP-LISTEN:<port>,fork UNIX:<socket file>
```