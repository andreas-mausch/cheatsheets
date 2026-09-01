---
layout: cheatsheet
tags: notify-send
---

Send desktop notification:

```
notify-send \
  --app-name="Test-Service" \
  --category="transfer.complete" \
  --urgency=normal \
  --icon="dialog-information" \
  --expire-time=5000 \
  --hint="string:sound-name:complete" \
  "Test-Notification" \
  "Just a test."
```

Other icons:

```
dialog-information
dialog-warning
dialog-error
dialog-question
document-new
document-save
edit-copy
edit-paste
system-search
media-playback-start
network-idle
network-offline
battery-low
battery-caution
firefox
vlc
```

You can also reference a local image file instead.

# References

Categories:
<https://galago-project.org/specs/notification/0.9/x211.html>
