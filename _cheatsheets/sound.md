---
layout: cheatsheet
tags: pacmd pactl audio hdmi alsa
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
---
