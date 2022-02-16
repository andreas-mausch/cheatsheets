---
layout: cheatsheet
tags: pacmd pactl audio pulseaudio hdmi alsa bluetooth bluetoothctl
section:
  - name: List
    commands:
       List cards: pacmd list-cards
       List sinks: pacmd list-sinks
       List sources: pacmd list-sources
       Via pactl: pactl list
  - name: Set audio sink
    commands:
       Output to HDMI: pactl set-card-profile 0 output:hdmi-stereo+input:analog-stereo
       Output back to normal: pactl set-card-profile 0 output:analog-stereo+input:analog-stereo
  - name: Bluetooth
    commands:
      Scan: bluetoothctl scan on
      List: bluetoothctl devices
      List paired devices: bluetoothctl paired-devices
      List connected devices (wow): bluetoothctl devices | cut -f2 -d' ' | while read uuid; bluetoothctl info $uuid; end|grep -e "Device\|Connected\|Name"
      Info for single device: bluetoothctl info <MAC>
      Connect: bluetoothctl connect <MAC>
      Disconnect: bluetoothctl connect <MAC>
      Trust: bluetoothctl trust <MAC>
      Pair: bluetoothctl pair <MAC>
      Unpair: bluetoothctl cancel-pairing <MAC>
      Remove: bluetoothctl remove <MAC>
      Switch audio output to bluetooth device: "pacmd set-default-sink 1 [or the name: bluez_sink.AA_BB_CC_DD_EE_FF.a2dp_sink]"
---
