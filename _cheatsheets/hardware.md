---
layout: cheatsheet
tags: dmidecode hwinfo ip mac lscpu lspci lsusb inxi
section:
  - name: General hardware information
    commands:
      "inxi (-F: full output, -x: add details, -z: mask personal info)": inxi -Fxz
      hwinfo: hwinfo --short
      BIOS: sudo dmidecode --type bios
      Model name: sudo dmidecode --string system-version
  - name: Update firmware
    commands:
      Display all detected devices: fwupdmgr get-devices
      Download latest metadata from LVFS: fwupdmgr refresh
      Display available updates: fwupdmgr get-updates
      Download and apply updates: fwupdmgr update
  - name: CPU
    commands:
      lscpu: lscpu
      dmidecode: sudo dmidecode --string processor-version
  - name: Memory
    commands:
      Show RAM speed: sudo dmidecode --type memory
  - name: Network
    commands:
      Find wireless card (WiFi / WLAN): lspci | grep -i "wireless\|wifi"
      Show details (replace the number returned by previous command): lspci -vv -s 53:00.0
      via lshw: lshw -C network
      Find physical network devices: ls -l /sys/class/net/ | grep -v virtual
      Show IP and MAC address: ip addr show
  - name: Show USB devices
    commands:
      List devices: lsusb [-v]
---
