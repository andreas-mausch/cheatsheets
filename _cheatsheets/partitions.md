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
      Item sizes, sorted: du -sh --apparent-size * | sort -h
  - name: lsblk
    commands:
      Determine filesystem: lsblk --fs --paths --perms --output=+TRAN
  - name: Flash img
    commands:
      xz: xzcat 2024-03-15-raspios-bookworm-armhf-lite.img.xz | sudo dd of=/dev/mmcbzz0 bs=1M oflag=sync status=progress
  - name: Backup
    commands:
      Backup SD card: sudo dd if=/dev/sdb of=./raspberrypi.dd.img bs=1M status=progress
  - name: Backup and zip
    commands:
      Backup and gzip: sudo dd if=/dev/X bs=1M | gzip > ./raspberrypi.dd.img.gz
      Restore: sudo gzip --decompress --to-stdout ./raspberrypi.dd.img.gz | sudo dd of=/dev/X bs=1M
  - name: Create new partition table (MBR) and exfat partition
    commands:
      Clear partition table and create new one: sudo parted /dev/sda --script mklabel msdos
      Create new partition: sudo parted /dev/sda --script mkpart primary 0% 100%
  - name: Same, but GPT partition table
    commands:
      Clear partition table and create new one: sudo parted /dev/sdb --script mklabel gpt
      Create new partition: sudo parted /dev/sdb --script mkpart MYLABEL 0% 100%
  - name: Create filesystem and verify result
    commands:
      Create filesystem: sudo mkfs.exfat -n MYLABEL /dev/sda1
      Verify partition table: sudo parted /dev/sda --script print
---

Careful with the commands above, they might erase
your drives permanently.
Double check you are using the correct device (e.g. `/dev/sda`).

Make sure you have a backup of all important data.
