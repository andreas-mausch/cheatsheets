---
layout: cheatsheet
tags: sysbench stress-ng
section:
  - name: stress-ng CPU
    commands:
      Single-core: stress-ng --cpu 1 --verify -t 10s --metrics-brief
      Multi-core: stress-ng --cpu 16 --verify -t 10s --metrics-brief
---
