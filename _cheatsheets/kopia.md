---
layout: cheatsheet
tags: backup
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgdmVyc2lvbj0iMS4yIgogICB2aWV3Qm94PSIwIDAgOTkuOTk5OTk4IDY0IgogICB3aWR0aD0iMTAwIgogICBoZWlnaHQ9IjY0IgogICBpZD0ic3ZnNyIKICAgc29kaXBvZGk6ZG9jbmFtZT0ia29waWEuc3ZnIgogICBpbmtzY2FwZTp2ZXJzaW9uPSIxLjIuMSAoOWM2ZDQxZSwgMjAyMi0wNy0xNCkiCiAgIGlua3NjYXBlOmV4cG9ydC1maWxlbmFtZT0ia29waWEtYXBwLTEwMjQucG5nIgogICBpbmtzY2FwZTpleHBvcnQteGRwaT0iOTYiCiAgIGlua3NjYXBlOmV4cG9ydC15ZHBpPSI5NiIKICAgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIKICAgeG1sbnM6aW5rc2NhcGU9Imh0dHA6Ly93d3cuaW5rc2NhcGUub3JnL25hbWVzcGFjZXMvaW5rc2NhcGUiCiAgIHhtbG5zOnNvZGlwb2RpPSJodHRwOi8vc29kaXBvZGkuc291cmNlZm9yZ2UubmV0L0RURC9zb2RpcG9kaS0wLmR0ZCIKICAgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIgogICB4bWxuczpzdmc9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIgogICB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiCiAgIHhtbG5zOmNjPSJodHRwOi8vY3JlYXRpdmVjb21tb25zLm9yZy9ucyMiCiAgIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyI+PGRlZnMKICAgICBpZD0iZGVmczExIiAvPjxzb2RpcG9kaTpuYW1lZHZpZXcKICAgICBpZD0ibmFtZWR2aWV3OSIKICAgICBwYWdlY29sb3I9IiNmZmZmZmYiCiAgICAgYm9yZGVyY29sb3I9IiMwMDAwMDAiCiAgICAgYm9yZGVyb3BhY2l0eT0iMC4yNSIKICAgICBpbmtzY2FwZTpzaG93cGFnZXNoYWRvdz0iMiIKICAgICBpbmtzY2FwZTpwYWdlb3BhY2l0eT0iMC4wIgogICAgIGlua3NjYXBlOnBhZ2VjaGVja2VyYm9hcmQ9InRydWUiCiAgICAgaW5rc2NhcGU6ZGVza2NvbG9yPSIjZDFkMWQxIgogICAgIHNob3dncmlkPSJmYWxzZSIKICAgICBpbmtzY2FwZTp6b29tPSIwLjcyOTEzNTUxIgogICAgIGlua3NjYXBlOmN4PSIxODUuMTUwNzciCiAgICAgaW5rc2NhcGU6Y3k9IjE5MS4zMjI0NiIKICAgICBpbmtzY2FwZTp3aW5kb3ctd2lkdGg9IjE0ODciCiAgICAgaW5rc2NhcGU6d2luZG93LWhlaWdodD0iODAxIgogICAgIGlua3NjYXBlOndpbmRvdy14PSIwIgogICAgIGlua3NjYXBlOndpbmRvdy15PSIzOCIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIwIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzciIC8+PHRpdGxlCiAgICAgaWQ9InRpdGxlMiI+a29waWEtc3ZnPC90aXRsZT48c3R5bGUKICAgICBpZD0ic3R5bGU0Ij4KCQkuczAgeyBmaWxsOiAjMmE3ZmZmIH0gCgk8L3N0eWxlPjxwYXRoCiAgICAgaWQ9IlNoYXBlIDEiCiAgICAgY2xhc3M9InMwIgogICAgIGQ9Ik0gMzEuNTU5NDEyLDE2LjEzOTM1OCBDIDQ3LjYxMDUxNSwtMTQuOTUyNjI5IDg5LjEwODQ5LDMuNzAyNTYzNCA4NS41ODUwNzUsMzEuNDc4MDczIGMgMTcuMjI1NTc1LDIuNDg3MzY0IDE3LjIyNTU3NSwzMi43NTAyMjMgLTEuOTU3NDUsMzIuNzUwMjIzIC00LjY5Nzg4MSwwLjQxNDU2OCAtMTkuNjQ2NzMyLDAuNDE0NTY4IC0xOS42NDY3MzIsMC40MTQ1NjggViA1MS4zNzY5NTEgTCA3Mi4yMDIxOTUsNDIuMjU2NjMyIDU4LjE4MDc1MiwxNS43MjQ4MDUgNDMuMTg3ODExLDQyLjI1NjYzMiA1MS44MDA1OTUsNTEuMzc2OTUxIFYgNjQuNjQyODY0IEggMTYuMjkxMjg5IGMgLTE4LjQwMDA0NTYsMCAtMjMuODgwOTExNCwtMzEuOTIxMTA4IC0yLjM0ODk0NSwtMzcuMzEwMzc1IC0wLjc4Mjk3OSwtNy40NjIwODMgNy40MzgzMTksLTE0LjkyNDE2MyAxNy4yMjU1NzUsLTExLjE5MzEyNSB6IgogICAgIHN0eWxlPSJmaWxsOiMyZjgwZmY7ZmlsbC1vcGFjaXR5OjE7c3Ryb2tlOm5vbmU7c3Ryb2tlLXdpZHRoOjAuNDQ4MzUxO3N0cm9rZS1saW5lam9pbjpyb3VuZDtzdHJva2UtZGFzaGFycmF5Om5vbmUiCiAgICAgc29kaXBvZGk6bm9kZXR5cGVzPSJjY2NjY2NjY2Njc2NjYyIgLz48bWV0YWRhdGEKICAgICBpZD0ibWV0YWRhdGExMDAwIj48cmRmOlJERj48Y2M6V29yawogICAgICAgICByZGY6YWJvdXQ9IiI+PGRjOnRpdGxlPmtvcGlhLXN2ZzwvZGM6dGl0bGU+PC9jYzpXb3JrPjwvcmRmOlJERj48L21ldGFkYXRhPjwvc3ZnPgo=
section:
  - name: Create repository
    commands:
      Create repo: kopia repository create filesystem --no-check-for-updates --ecc=REED-SOLOMON-CRC32 --ecc-overhead-percent=5 --encryption=AES256-GCM-HMAC-SHA256 --path '/mnt/kopia-backup/kopia'
      Validate provider: kopia repository validate-provider
      Show status: kopia repository status --json | jq
      Keep all snapshots forever: kopia policy set /mnt/nas --keep-latest=0 --keep-hourly=0 --keep-daily=0 --keep-weekly=0 --keep-monthly=0 --keep-annual=0
      Ignore file pattern: kopia policy set /mnt/nas --add-ignore 'lost+found'
      List policies: kopia policy list
      Show policies: kopia policy show /mnt/nas
      Disable automatic maintenance: kopia maintenance set --enable-quick=false --enable-full=false
  - name: New snapshot
    commands:
      Connect: kopia repository connect filesystem --no-check-for-updates --path '/mnt/kopia-backup/kopia'
      Create snapshot: kopia snapshot create /mnt/nas/
      List snapshots: kopia snapshot list --all --storage-stats
      Content stats: kopia content stats
      Blob stats: kopia blob stats
  - name: Inspect snapshot
    commands:
      List files in snapshot: kopia ls -l kbdae7e8xxx
      Mount specific snapshot: kopia mount kbdae7e8xxx /tmp/mnt-kopia/
      Mount all: kopia mount all /tmp/mnt-kopia/
  - name: Validate
    commands:
      Full validation: kopia snapshot verify --verify-files-percent=100 --file-parallelism=10 --parallel=10
---

Unfortunately, the [error correction](https://kopia.io/docs/advanced/ecc/) is still not stable for over a year now.

[This post](https://kopia.discourse.group/t/error-correction-algorithm-questions/1585) mentions the project
is not actively maintained. :(

Full list of commands to create a new snapshot:

```bash
lsblk --fs --perms --paths
sudo mount /dev/sdb1 /mnt/kopia-backup/
kopia repository connect filesystem --no-check-for-updates --path '/mnt/kopia-backup/kopia/'
kopia snapshot create /mnt/nas/
kopia snapshot list --all --storage-stats
sync
sudo umount /mnt/kopia-backup
sudo udisksctl power-off -b /dev/sdb
```
