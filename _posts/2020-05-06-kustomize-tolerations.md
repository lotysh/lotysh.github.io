---
layout: post
title: "Using kustomize to modify tolerations "
date: 2023-01-31
---

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
