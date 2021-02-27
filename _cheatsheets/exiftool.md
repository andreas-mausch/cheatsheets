---
layout: cheatsheet
tags: image-processing exif
section:
  - name: Print
    commands:
      Print raw tag names: "exiftool -s <FILENAME>"
      Print values only: "exiftool -s3 <FILENAME>"
      Print camera models: exiftool -model -s3 -r .
  - name: Find
    commands:
      Find files without exif data: "exiftool -s3 -filepath -q -if 'not $exif:all' -r <YOUR_DIRECTORY_TO_SCAN>"
      Find all pictures edited with Snapseed: "exiftool -if '$software =~ /snapseed/i' -p '$directory/$filename' -r -q -q ."
---
