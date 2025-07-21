---
layout: cheatsheet
tags: v4l2 camera uvc video
section:
  - name: List devices and formats
    commands:
      List devices: v4l2-ctl --list-devices
      List formats for a specific device: v4l2-ctl --device /dev/video0 --list-formats-ext
      Use ffmpeg: ffmpeg -f video4linux2 -list_formats all -i /dev/video0
---
