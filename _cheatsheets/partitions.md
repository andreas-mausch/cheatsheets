---
layout: cheatsheet
tags: dd df du lsblk disk space size backup
section:
  - name: df
    commands:
      Free disk space: df -h
  - name: du
    commands:
      Folder size: du -sh --apparent-size .
  - name: lsblk
    commands:
      Determine filesystem: lsblk -f
  - name: Backup
    commands:
      Backup SD card: sudo dd if=/dev/sdb of=./raspberrypi.dd.img bs=1M status=progress
---
