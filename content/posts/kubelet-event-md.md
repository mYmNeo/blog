---
title: kubernetes-memo.md
date: 2017-09-14 10:05:25
tags:
    - linux
    - kubernetes
---
# Kubernetes

<!-- more -->
## kubelet event
|PLEG|Apiserver|PodOperation|SyncPodType|Reason|Action
|----|----|----|----|----|----
||SET|ADD|SyncPodCreate|Pod is first found|HandlePodAdditions
|||UPDATE|SyncPodUpdate|Pod has semantical difference|HandlePodUpdates
|||RECONCILE||Pod has semantical difference and its status not equal to last circle|HandlePodReconcile
|||DELETE|SyncPodUpdate|Pod has DeletionTimestamp|HandlePodUpdates
|||REMOVE||Pos is not found in last circle|HandlePodRemoves
|ContainerStarted|||SyncPodSync|Container start|HandlePodSyncs
|ContainerDied|||SyncPodSync|Container exited|HandlePodSyncs
|ContainerChanged|||SyncPodSync|Container changed|HandlePodSyncs