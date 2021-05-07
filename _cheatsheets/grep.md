---
layout: cheatsheet
tags: search
section:
  - name: Search file contents
    commands:
      Find string in files: grep --ignore-case --recursive --no-messages --exclude-dir=node_modules --exclude-dir=dist --exclude-dir=build --exclude-dir=.git --exclude=package-lock.json "<your string>" .
---
