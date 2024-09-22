---
layout: cheatsheet
tags: backup
section:
  - name: Backup
    commands:
      Create repo: kopia repository create filesystem --path "/run/media/BKP2024-02/kopia/"
      Create snapshot: kopia snapshot create "/my/source/folder/"
      Validate provider: kopia repository validate-provider
      Mute update warnings: rm ~/.config/kopia/repository.config.update-info.json
  - name: Restore
    commands:
      Connect: kopia repository connect filesystem --path "/run/media/BKP2024-02/kopia/"
      List snapshots: kopia snapshot list --all
      List files in snapshot: kopia ls -l kbdae7e8xxx
      Mount specific snapshot: kopia mount kbdae7e8xxx /tmp/mnt-kopia/
      Mount all: kopia mount all /tmp/mnt-kopia/
  - name: Validate
    commands:
      Full validation: kopia snapshot verify --verify-files-percent=100 --file-parallelism=10 --parallel=10
      Disable automatic maintenance: kopia maintenance set --enable-quick=false --enable-full=false
  - name: Policy
    commands:
      List policies: kopia policy list
      Ignore file patterns: kopia policy set --add-ignore .npm/ --add-ignore node_modules/ --global
---

Unfortunately, the [error correction](https://kopia.io/docs/advanced/ecc/) is still not stable for over a year now.

[This post](https://kopia.discourse.group/t/error-correction-algorithm-questions/1585) mentions the project
is not actively maintained. :(
