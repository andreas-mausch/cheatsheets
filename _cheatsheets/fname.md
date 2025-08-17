---
layout: cheatsheet
tags: random username
section:
  - name: Create a random username
    commands:
      Adjective, Substantive, 4 digits: echo "$(fname --casing title --delimiter '')$(cat /dev/random | tr -dc '1234567890' | head -c 4)"
---
