---
layout: cheatsheet
section:
  - name: Filter GPX file by date
    commands:
      Filter: gpsbabel -i gpx -f 2020-06-14_.gpx -x track,start=20200611000000,stop=20200614235959 -o gpx -F out.gpx
---
