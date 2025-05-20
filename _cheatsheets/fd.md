---
layout: cheatsheet
tags: filetypes files search
section:
  - name: File types
    commands:
      Largest files: fd -t f -X du -Sh | sort -rh | head -n 10
  - name: Last change
    commands:
      Show all files changed within the last year: fd --changed-within 1year -l
      Show all files which are older than one year: fd --change-older-than 1year -l
---
