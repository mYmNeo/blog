---
title: port forwarding in windows
date: 2017-03-10 21:25:25
tags:
    - windows
    - netsh
---

# Port forwarding configuration

1. Add rule  
- forward A:B to C:D
```
netsh interface portproxy add v4tov4 listenaddress=A listenport=B connectaddress=C connectport=D
```
2. Delete rule
- delete A:B
```
netsh interface portproxy delete v4tov4 listenaddress=A listenport=B
```
3. List all rules
```
netsh interface portproxy show all
```