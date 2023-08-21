---
layout: cheatsheet
tags: extended attributes file
section:
  - name: Get & Set
    commands:
      Set a user attribute: setfattr -n user.tags -v "This is a test" ./testfile
      List all attributes with its values: getfattr --dump ./testfile
  - name: Find
    commands:
      Find all files with a specific attribute value: getfattr --recursive --dump . | grep -B 2 "This is a test"
---
