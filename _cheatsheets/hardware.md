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
  - name: CPU
    commands:
      lscpu: lscpu
      dmidecode: sudo dmidecode --string processor-version
  - name: Memory
    commands:
      Show RAM speed: sudo dmidecode --type memory
  - name: Network
    commands:
      Find wireless card (WiFi / WLAN): lspci | grep -i wireless
      Show details (replace the number returned by previous command): lspci -vv -s 53:00.0
      Show IP and MAC address: ip addr show
  - name: Show USB devices
    commands:
      List devices: lsusb [-v]
---
