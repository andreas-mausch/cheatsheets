---
layout: cheatsheet
tags: extended attributes file
section:
  - name: Get & Set
    commands:
      Set a user attribute: setfattr -n user.tags -v "This is a test" ./testfile
      List all attributes with its values: getfattr --dump ./testfile
---
