---
layout: cheatsheet
tags: backup
section:
  - name: Restore
    commands:
      Connect: kopia repository connect filesystem --path "/run/media/BKP2024-02/kopia/"
      List snapshots: kopia snapshot list --all
      Mount specific snapshot: kopia mount kbdae7e8xxx /tmp/mnt-kopia/
      Mount all: kopia mount all /tmp/mnt-kopia/
---
