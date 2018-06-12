---
title: resize disk
date: 2016-06-13 14:39:06
tags:
    - linux
    - filesystem
    - cheatsheet
---
# Shrink a disk
1. If the partition the file system is on is currently mounted, unmount it
```bash
umount /dev/disk
```
<!-- more -->
1. Run fsck on the umounted file system
```bash
e2fsck -f /dev/disk
```
1. Shrink the file system with the `resize2fs /dev/fdisk size`
```bash
resize2fs /dev/disk size
```
1. Use `fdisk` to modify the partition table information
```bash
fdisk /dev/disk
```
1. Mount the disk
```bash
mount /dev/disk target
```