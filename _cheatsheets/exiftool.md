---
layout: cheatsheet
tags: image-processing exif gps gpx tracking
section:
  - name: Print
    commands:
      Print raw tag names: "exiftool -s <FILENAME>"
      Print values only: "exiftool -s3 <FILENAME>"
      Print camera models: exiftool -model -s3 -r .
      Print jpeg structure (markers): exiv2 -pS image.jpg
      Print image structure recursively (tiff, only on debug build): exiv2 -pR image.jpg
      Print all tags: exiv2 -pa image.jpg
  - name: Find
    commands:
      Find files without exif data: "exiftool -s3 -filepath -q -if 'not $exif:all' -r <YOUR_DIRECTORY_TO_SCAN>"
      Find all pictures edited with Snapseed: "exiftool -if '$software =~ /snapseed/i' -p '$directory/$filename' -r -q -q ."
  - name: Location
    commands:
      Print GPS coordinates: exiftool -if '$gpslatitude' -a "-gps*" -ee -c "%.6f degrees" image.jpg
      Create .gpx track from images (via gpx.fmt): "exiftool -if '$datetimeoriginal' -fileOrder datetimeoriginal -d \"%Y-%m-%dT%H:%M:%S+02:00\" -p ./gpx.fmt ./*.jpg > output.gpx"
  - name: Thumbnail
    commands:
      List thumbnails: exiftool -a -preview:all image.jpg
      Extract all types of preview images: "exiftool -a -b -W %d%f_%t%-c.%s -preview:all image.jpg"
  - name: XMP
    commands:
      Show raw xmp xml data (exiftool): exiftool -xmp -b image.jpg
      Show raw xmp xml data (exiv2): exiv2 -pX image.jpg
---

- -a: Allow duplicate tags to be extracted
- -b: Output requested metadata in binary format
- -d: Set format for date/time values
- -p: Print output in specified format
- -s: Short output format (To see the tag names instead of the descriptions, use -s)
- -s3: Print values only (no tag names)
- -W: With -W, a new output file is created for each extracted tag

*gpx.fmt*

```
#------------------------------------------------------------------------------
# File:         gpx.fmt
#
# Description:  Example ExifTool print format file to generate a GPX track log
#
# Usage:        exiftool -p gpx.fmt -ee FILE [...] > out.gpx
#
# Requires:     ExifTool version 10.49 or later
#
# Revisions:    2010/02/05 - P. Harvey created
#               2018/01/04 - PH Added IF to be sure position exists
#               2018/01/06 - PH Use DateFmt function instead of -d option
#               2019/10/24 - PH Preserve sub-seconds in GPSDateTime value
#
# Notes:     1) Input file(s) must contain GPSLatitude and GPSLongitude.
#            2) The -ee option is to extract the full track from video files.
#            3) The -fileOrder option may be used to control the order of the
#               generated track points when processing multiple files.
#------------------------------------------------------------------------------
#[HEAD]<?xml version="1.0" encoding="utf-8"?>
#[HEAD]<gpx version="1.0"
#[HEAD] creator="ExifTool $ExifToolVersion"
#[HEAD] xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
#[HEAD] xmlns="http://www.topografix.com/GPX/1/0"
#[HEAD] xsi:schemaLocation="http://www.topografix.com/GPX/1/0 http://www.topografix.com/GPX/1/0/gpx.xsd">
#[HEAD]<trk>
#[HEAD]<number>1</number>
#[HEAD]<trkseg>
#[IF]  $gpslatitude $gpslongitude
#[BODY]<trkpt lat="$gpslatitude#" lon="$gpslongitude#">
#[BODY]  <ele>$gpsaltitude#</ele>
#[BODY]  <time>${gpsdatetime#;my ($ss)=/\.\d+/g;DateFmt("%Y-%m-%dT%H:%M:%SZ");s/Z/${ss}Z/ if $ss}</time>
#[BODY]</trkpt>
#[TAIL]</trkseg>
#[TAIL]</trk>
#[TAIL]</gpx>
```
