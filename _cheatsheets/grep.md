---
layout: cheatsheet
tags: search
section:
  - name: Search file contents
    commands:
      - title: Find string in files
        command: grep --ignore-case --recursive --no-messages --exclude-dir=node_modules --exclude-dir=dist --exclude-dir=build --exclude-dir=.git --exclude=package-lock.json "<your string>" .
      - title: Show filenames only
        command: grep -rils "<your string>" .
        options:
          -r: --recursive
          -i: --ignore-case
          -l: "--files-with-matches: Suppress normal output; instead print the name of each input file from which output would normally have been printed."
          -s: "--no-messages: Suppress error messages about nonexistent or unreadable files. (This hides 'Permission denied' spam)"
---
