---
title: ssh tunnel configuration
date: 2018-06-29 10:31:00
tags: 
    - linux
    - ssh
---

# SSH Tunnel Configuration

You basically have three possibilities:

- Tunnel from localhost to host1:

```
ssh -L 9999:host2:1234 -N host1
```

As noted above, the connection from host1 to host2 will not be secured.

- Tunnel from localhost to host1 and from host1 to host2:

```
ssh -L 9999:localhost:9999 host1 ssh -L 9999:localhost:1234 -N host2
```

This will open a tunnel from localhost to host1 and another tunnel from host1 to host2. However the port 9999 to host2:1234 can be used by anyone on host1. This may or may not be a problem.

- Tunnel from localhost to host1 and from localhost to host2:

```
ssh -L 9998:host2:22 -N host1
ssh -L 9999:localhost:1234 -N -p 9998 localhost
```

This will open a tunnel from localhost to host1 through which the SSH service on host2 can be used. Then a second tunnel is opened from localhost to host2 through the first tunnel.

Normally, I'd go with option 1. If the connection from host1 to host2 needs to be secured, go with option 2. Option 3 is mainly useful to access a service on host2 that is only reachable from host2 itself.