---
layout: cheatsheet
tags: sysbench stress-ng
section:
  - name: stress-ng CPU
    commands:
      Single-core: stress-ng --cpu 1 --verify -t 10s --metrics-brief
      Multi-core: stress-ng --cpu 16 --verify -t 10s --metrics-brief
---

# Results

stress-ng results are in *bogo ops/s in real time*.

| **Tool**  | **Version** | **CPU**                              | **Single-core** | **Multi-core** |
|-----------|-------------|--------------------------------------|-----------------|----------------|
| stress-ng | 0.20.01     | AMD Ryzen 7 PRO 7840U                | 2224            | 23103          |
| stress-ng | 0.20.01     | Intel Core i5-7Y54 (MacBook 12 2017) | 1383            | 3463           |
