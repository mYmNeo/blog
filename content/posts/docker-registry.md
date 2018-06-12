---
title: docker registry
date: 2016-04-27 22:35:19
tags: 
    - docker
---
+ search v1 repository list
```bash
curl http://registry.com/v1/search
```
<!-- more -->
+ pull image
```bash
docker pull <hub address>/<name>
```
+ push image
```bash
docker tag <image id or image name> <hub address>/<name>:<version>
docker push <hub address>/<name>:<version>
```
+ save image
```bash
docker save -o <filename> <image id or image name>
```
+ load image
```bash
docker load -i <filename>
```