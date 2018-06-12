---
title: behaviors of ext4 file system when devicemapper pool is full
date: 2016-06-23 17:41:46
tags:
    - linux
    - devicemapper
    - docker
---
# Backgroud
&nbsp;&nbsp;&nbsp;&nbsp;Our production system currently use docker to run all kinds of services. One day our clients reported that their service could not write down any log in the container and all the other containers which were started and worked well a few days ago also couldn't. And the containers couldn't be recovered. We logged in the malfunction machine, found that the thin pool used by devicemapper was full. At the same time there was some messages that `dmesg` reported telling the file system of containers became read-only.

# Reason
&nbsp;&nbsp;&nbsp;&nbsp;Devicemapper is a COW storage model, that means no blocks are allocated if no data is produced. A container had 10G capacity as default. Now we assume that your thin pool's size is 40G, and 4 containers writing log persistently and rapidly, the last 5 produce data very slowly. At some moment, the pool becomes full because of that 4 containers which generate log persistently and rapidly. And this time it triggers the condition we mentioned at the beginning of the article, all the 10 containers become read-only, we can't recover them except we delete them.

&nbsp;&nbsp;&nbsp;&nbsp;The reason why the conainer became read-only is that the error behavior of file system. When the pool is full, a request of allocating a block in thin pool will failed, that will raise an error to file system. The default hanlder to this kind of error of `ext4` is to remount the file system read-only.

# Prevention
&nbsp;&nbsp;&nbsp;&nbsp;Add surveillance to thin pool used by devicemapper.