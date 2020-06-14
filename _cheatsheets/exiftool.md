---
layout: cheatsheet
tags: image-processing exif
section:
  - name: Find
    commands:
      Find files without exif data: "exiftool -s3 -filepath -q -if 'not $exif:all' -r <YOUR_DIRECTORY_TO_SCAN>"
      Find camera models: exiftool -model -s3 -r .
---
