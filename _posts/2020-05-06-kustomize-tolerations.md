---
layout: post
title: "Using kustomize to modify tolerations "
date: 2023-01-31
---

Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes. One or more taints are applied to a node; this marks that the node should not accept any pods that do not tolerate the taints. Tolerations are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints.

Kustomize supports modifying a pod from a base by adding pod tolerations. You can use a strategic merge patch to add it.

```
      - op: add
        path: "/spec/template/spec/tolerations"
        value: []
      - op: add
        path: "/spec/template/spec/tolerations/-"
        value:
          key: service
          operator: Equal
          value: your-service
          effect: NoSchedule
      - op: add
        path: "/spec/template/spec/tolerations/-"
        value:
          effect: "NoExecute"
          key: node.kubernetes.io/not-ready
          operator: Exists
          tolerationSeconds: 300
      - op: add
        path: "/spec/template/spec/tolerations/-"
        value:
          effect: "NoExecute"
          key: node.kubernetes.io/unreachable
          operator: Exists
          tolerationSeconds: 300     

```
