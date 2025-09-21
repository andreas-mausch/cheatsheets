---
layout: cheatsheet
tags: backup websites warc archivebox httrack
section:
  - name: archivebox
    commands:
      Init: docker run -it -v $PWD:/data archivebox/archivebox init --setup
      Backup website: docker run -it -v $PWD:/data archivebox/archivebox add https://google.com
  - name: httrack
    commands:
      Backup website: httrack "https://google.com" -O "/tmp/google.com" "+*.google.com/*" -v
---
