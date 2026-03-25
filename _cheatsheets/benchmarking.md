---
layout: cheatsheet
tags: sysbench stress-ng
section:
  - name: stress-ng CPU
    commands:
      Single-core: stress-ng --cpu=1 --cpu-method=sqrt --timeout=10s --verify --metrics-brief
      Multi-core: stress-ng --cpu=0 --cpu-method=sqrt --timeout=10s --verify --metrics-brief
---

# Results

stress-ng results are in *bogo ops/s in real time*.

Tests are run on battery mode in balanced or powersave profile.

| **Tool**  | **Version** | **Model**        | **CPU**               | **Single-core** | **Multi-core** |
|-----------|-------------|------------------|-----------------------|-----------------|----------------|
| stress-ng | 0.20.01     | Lenovo P14s      | AMD Ryzen 7 PRO 7840U | 2.254           | 23.663         |
| stress-ng | 0.20.01     | MacBook 12 2017  | Intel Core i5-7Y54    | 1.123           | 2.559          |
| stress-ng | 0.20.01     | Dell XPS 13 9310 | Intel Core i7-1185G7  | ?               | ?              |
| stress-ng | 0.20.01     | MacBook Air 2020 | M1                    | 3.099           | 18.486         |
