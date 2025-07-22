---
layout: cheatsheet
tags: rm delete securely erase
section:
  - name: Delete files forever!
    commands:
      Recursively delete all files: find . -type f -exec shred --verbose --random-source=/dev/urandom --iterations=1 --remove "{}" \;
---

Be very careful when using this!

Be also especially careful with filesname having special characters, like spaces or newlines.
