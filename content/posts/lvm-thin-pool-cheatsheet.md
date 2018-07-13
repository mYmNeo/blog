---
title: lvm thin pool cheatsheet
date: 2016-06-13 15:17:34
tags:
    - linux
    - devicemapper
    - docker
    - cheatsheet
---
> We use devicemapper as Docker storage driver, sometime any of the meta or data pool is full. We have to extend the pool

1. Single step thin pool LV creation

```bash
lvcreate --type thin-pool --poolmetadata <meta size> -L <pool size> <pool name>
```

1. Manually manage free data space of thin pool LV

```bash
lvextend -L <size> <pool name>
```

1. Manually manage free metadata space of a thin pool LV

```bash
lvs -oname,size,data_percent,metadata_percent # show the available metadat space in a thin pool LV
lvextend --poolmetadatasize <size> <pool name>
```

## Metadata space exhaustion
>Metadata space exhaustion can lead to inconsistent thin pool metadata
>and inconsistent file systems, so the response requires offline
>checking and repair.

1. Deactivate the thin pool LV, or reboot the system if this is not possible.
1. Repair thin pool with `lvconvert --repair`. See "Metadata check and repair".
1. Extend pool metadata space with `lvextend --poolmetadatasize`.
1. Check and repair file system with fsck.

## Metadata check and repair
Repair performs the following steps:
1. Creates a new, repaired copy of the metadata.lvconvert runs the thin_repair command to read damaged metadata from the existing pool metadata LV, and writes a new repaired copy to the VG's pmspare LV.
2. Replaces the thin pool metadata LV.
If step 1 is successful, the thin pool metadata LV is replaced with
the pmspare LV containing the corrected metadata.  The previous thin
pool metadata LV, containing the damaged metadata, becomes visible
with the new name ThinPoolLV_tmetaN (where N is 0,1,...).

If the repair works, the thin pool LV and its thin LVs can be
activated, and the LV containing the damaged thin pool metadata can
be removed.  It may be useful to move the new metadata LV (previously
pmspare) to a better PV.

If the repair does not work, the thin pool LV and its thin LVs are
lost.

If metadata is manually restored with thin_repair directly, the pool
metadata LV can be manually swapped with another LV containing new
metadata:
`lvconvert --thinpool VG/ThinPoolLV --poolmetadata VG/NewThinMetaLV`
