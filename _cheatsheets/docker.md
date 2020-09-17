---
layout: cheatsheet
tags:
section:
  - name: stats
    commands:
      sort by memory usage: docker stats --no-stream --format "table {{.Name}}\t{{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}" | LC_ALL=en_US.utf8 sort -k 4 -h
---
