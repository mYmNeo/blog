---
title: kvm virtual machine with vnc support
date: 2016-06-22 16:32:51
tags:
    - kvm
    - linux
---

# Install a KVM virtual machin with VNC support
1. Create a disk for VM
```bash
qemu-img create -f qcow2 <img path> <size>
```
<!-- more -->
1. Use virt-install install a VM
```bash
virt-install \
    --virt-type kvm \
    --name <name> \
    --cdrom=<cdrom iso> \
    --disk path=<disk path> \
    --network network=default \
    --graphics vnc,listen=0.0.0.0 \
    --noautoconsole \
    --os-type=<os type> \
    --os-variant=<os>
```
1. Show VNC port
```bash
virsh vncdisplay <domain name>
```
### VM Operations

> Sometimes you need add <hypervisor connection URI>  
> For example:  
> virsh -c qemu:///system

- Start VM
```bash
virsh start <domain name>
```
- Stop VM
```bash
virsh destroy <domain name>
```
- Delete VM
```bash
virsh undefined <domain name>
```
