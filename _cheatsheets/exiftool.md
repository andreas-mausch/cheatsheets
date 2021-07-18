---
layout: cheatsheet
tags: image-processing exif gps gpx tracking
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
  - name: Location
    commands:
      Create .gpx track from images (via gpx.fmt): "exiftool -if '$datetimeoriginal' -fileOrder datetimeoriginal -d \"%Y-%m-%dT%H:%M:%S+02:00\" -p ./gpx.fmt ./*.jpg > output.gpx"
---
