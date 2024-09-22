---
layout: cheatsheet
tags: rm delete securely erase
section:
  - name: Delete files forever!
    commands:
      - title: Recursively delete all files
        command: find . -type f -exec shred -uvz -n1 {} \;
        options:
          -u: "--remove: truncate and remove file after overwriting"
          -v: --verbose
          -z: "--zero: add a final overwrite with zeros to hide shredding"
          -n: "--iterations: overwrite N times instead of the default (3)"
---

Be very careful when using this!

Be also especially careful with filesname having special characters, like spaces or newlines.
