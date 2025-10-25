---
layout: cheatsheet
tags: dmidecode hwinfo ip mac lscpu lspci lsusb inxi nmcli
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
      via lshw: sudo lshw -class network -short
      Find physical network devices: ls -l /sys/class/net/ | grep -v virtual
      Show IP and MAC address: ip addr show
      Show IP address only: ip -br a
      Find WiFis: nmcli dev wifi
  - name: Disks
    commands:
      via lshw: sudo lshw -class disk -short
      via inxi: sudo inxi -Dxxd
      via udevadm: bash -c 'for dev in /dev/sd? /dev/nvme?n1; do udevadm info --query=all --name="$dev" | grep -E "DEVNAME|ID_SERIAL"; echo ---; done'
      via nvme: nvme list
  - name: Show USB devices
    commands:
      List devices: lsusb [--tree --verbose]
---
