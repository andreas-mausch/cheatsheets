---
layout: cheatsheet
tags: image-processing exif gps gpx tracking
logo: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADICAYAAACtWK6eAAAC1klEQVR4nOzdUUokMRRAUTO4jp79L0s3kvmR+dILPVabTPqcf+GVeCFQz9TrnPMF+Nyv1QPAzgQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEF5XD/CJ2+oBNvO+eoBntmMgL2OMt9Uz7GDO+Xv1DM/OEQuCQCAIBIJAIAgEgkAgCASCQCAIBIJAIAgEgkAgbLms+B1zznHnj9ge5kvHBfIPrJPzJUcsCAKBIBAIAoEgEAgCgSAQCN6D3M+LxZ+19D3ViYHcHvhLvbmS6Gd9XH20LBJHLAgCgSAQCAKBIBAIAoEgEAgCgSAQCAKBIBAIAoEgEAgnbvM+dPNz1w9rfnfLeNfnWu3EQB5p1zu0rvoflV2fbxlHLAgCgSAQCAKBIBAIAoEgEAgCgfAMLwr/94vevLxb6LhAxhhz9QxXsf6xniMWBIFAEAgEgUAQCASBQBAIBIFAEAgEgUAQCASBQDhuWdGCH1c6LpAPVsS5hCMWBIFAEAgEgUAQCASBQBAIBIFAEAgEgUAQCASBQBAIBIFAEAgEgUAQCASBQBAIBIFAEAgEgUAQCASBQBAIBIFAEAgEgUAQCASBQBAIBIFAEAgEgUAQCIRTv1F4Wz3AhXxvcaHjAhljvK2e4Sq+2LueIxYEgUAQCASBQBAIBIFAEAgEgUAQCASBQBAIBIFAEAiEHbd5322x/mXVfbEdA3nxh8EuHLEgCASCQCAIBIJAIAgEgkAgCASCQCAIBIJAIAgEgkAgCASCQCAIBIJAIAgEgkAgCASCQCDseqsJd3JV0mOMOefqGWBbjlgQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEAQCQSAQBAJBIBAEAkEgEP4EAAD//yN2OIYOHW/tAAAAAElFTkSuQmCC
section:
  - name: Print
    commands:
      Print raw tag names: "exiftool -short -groupNames1 -duplicates <FILENAME>"
      Print values only: "exiftool -s3 <FILENAME>"
      Print camera models: exiftool -model -s3 -recurse .
      Print jpeg structure (markers): exiv2 -pS image.jpg
      Print image structure recursively (tiff, only on debug build): exiv2 -pR image.jpg
      Print all tags: exiv2 -pa image.jpg
  - name: Find
    commands:
      Find files without exif data: "exiftool -s3 -filepath -q -if 'not $exif:all' -r <YOUR_DIRECTORY_TO_SCAN>"
      Find all pictures edited with Snapseed: "exiftool -if '$software =~ /snapseed/i' -p '$directory/$filename' -r -q -q ."
      Find all pictures from selfie camera (Samsung S10): "exiftool -recurse -if '$FNumber eq \"1.9\" and $FocalLength eq \"3.3 mm\"' -printFormat '$directory/$filename' -quiet -quiet ."
      Find all pictures from selfie camera (Samsung A40): "exiftool -recurse -if '$FNumber eq \"2.0\" and $FocalLength eq \"3.8 mm\"' -printFormat '$directory/$filename' -quiet -quiet ."
  - name: Date and time
    commands:
      Change timezone (change to Havanna): exiftool "-SubSecDateTimeOriginal<\${DateTimeUTC;ShiftTime('-4:0:0')}" image.jpg
      Set exif timestamp to mdate: exiftool "-DateTimeOriginal<FileModifyDate" "-FileModifyDate<FileModifyDate" image.jpg
      Set mdate to exif timestamp: exiftool "-FileModifyDate<DateTimeOriginal" image.jpg
      Relative time change (+1 year, 12 month, 28 days, 14 hours, 54 minutes, 32 seconds): exiftool -DateTimeUTC-="1:12:28 14:54:32" -AllDates-="1:12:28 14:54:32" -verbose image.jpg
  - name: Location
    commands:
      Print GPS coordinates: exiftool -if '$gpslatitude' -a "-gps*" -ee -c "%.6f degrees" image.jpg
      Create .gpx track from images (via gpx.fmt): "exiftool -if '$datetimeoriginal' -fileOrder datetimeoriginal -d \"%Y-%m-%dT%H:%M:%S+02:00\" -p ./gpx.fmt ./*.jpg > output.gpx"
      Find files with GPS tags and display them in GPXSee: exiftool --recursive -q -q -if '$GPSLatitude' -p '$directory/$filename' . | xargs gpxsee
  - name: Thumbnail
    commands:
      List thumbnails: exiftool -a -preview:all image.jpg
      Extract all types of preview images: "exiftool -a -b -W %d%f_%t%-c.%s -preview:all image.jpg"
  - name: XMP
    commands:
      Show raw xmp xml data (exiftool): exiftool -xmp -binary image.jpg
      Show raw xmp xml data (exiv2): exiv2 -pX image.jpg
---

## Options

- -a: Allow duplicate tags to be extracted
- -b: Output requested metadata in binary format
- -d: Set format for date/time values
- -p: Print output in specified format
- -s: Short output format (To see the tag names instead of the descriptions, use -s)
- -s3: Print values only (no tag names)
- -W: With -W, a new output file is created for each extracted tag

## Date and Time

For Date/Time changes, see also
[https://superuser.com/questions/1757307/how-to-set-an-images-date-and-time-with-timezone-with-exiftool](https://superuser.com/questions/1757307/how-to-set-an-images-date-and-time-with-timezone-with-exiftool) here.

Note on **SubSecDateTimeOriginal**: It is a composite tag of *EXIF:DateTimeOriginal*, *SubSecTimeOriginal* and *OffsetTimeOriginal*.

There is also **AllDates**, see [here](https://exiftool.org/TagNames/Shortcuts.html).

**DateTimeUTC** seems to be used only on my Olympus camera.

## gpx.fmt

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
