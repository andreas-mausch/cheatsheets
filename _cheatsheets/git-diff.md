---
layout: cheatsheet
tags: vcs history changes
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4NCjwhLS0gR2VuZXJhdG9yOiBBZG9iZSBJbGx1c3RyYXRvciAxNi4wLjAsIFNWRyBFeHBvcnQgUGx1Zy1JbiAuIFNWRyBWZXJzaW9uOiA2LjAwIEJ1aWxkIDApICAtLT4NCjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+DQo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4Ig0KCSB3aWR0aD0iOTdweCIgaGVpZ2h0PSI5N3B4IiB2aWV3Qm94PSIwIDAgOTcgOTciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDk3IDk3IiB4bWw6c3BhY2U9InByZXNlcnZlIj4NCjxnPg0KCTxwYXRoIGZpbGw9IiNGMDUxMzMiIGQ9Ik05Mi43MSw0NC40MDhMNTIuNTkxLDQuMjkxYy0yLjMxLTIuMzExLTYuMDU3LTIuMzExLTguMzY5LDBsLTguMzMsOC4zMzJMNDYuNDU5LDIzLjE5DQoJCWMyLjQ1Ni0wLjgzLDUuMjcyLTAuMjczLDcuMjI5LDEuNjg1YzEuOTY5LDEuOTcsMi41MjEsNC44MSwxLjY3LDcuMjc1bDEwLjE4NiwxMC4xODVjMi40NjUtMC44NSw1LjMwNy0wLjMsNy4yNzUsMS42NzENCgkJYzIuNzUsMi43NSwyLjc1LDcuMjA2LDAsOS45NThjLTIuNzUyLDIuNzUxLTcuMjA4LDIuNzUxLTkuOTYxLDBjLTIuMDY4LTIuMDctMi41OC01LjExLTEuNTMxLTcuNjU4bC05LjUtOS40OTl2MjQuOTk3DQoJCWMwLjY3LDAuMzMyLDEuMzAzLDAuNzc0LDEuODYxLDEuMzMyYzIuNzUsMi43NSwyLjc1LDcuMjA2LDAsOS45NTljLTIuNzUsMi43NDktNy4yMDksMi43NDktOS45NTcsMGMtMi43NS0yLjc1NC0yLjc1LTcuMjEsMC05Ljk1OQ0KCQljMC42OC0wLjY3OSwxLjQ2Ny0xLjE5MywyLjMwNy0xLjUzN1YzNi4zNjljLTAuODQtMC4zNDQtMS42MjUtMC44NTMtMi4zMDctMS41MzdjLTIuMDgzLTIuMDgyLTIuNTg0LTUuMTQtMS41MTYtNy42OTgNCgkJTDMxLjc5OCwxNi43MTVMNC4yODgsNDQuMjIyYy0yLjMxMSwyLjMxMy0yLjMxMSw2LjA2LDAsOC4zNzFsNDAuMTIxLDQwLjExOGMyLjMxLDIuMzExLDYuMDU2LDIuMzExLDguMzY5LDBMOTIuNzEsNTIuNzc5DQoJCUM5NS4wMjEsNTAuNDY4LDk1LjAyMSw0Ni43MTksOTIuNzEsNDQuNDA4eiIvPg0KPC9nPg0KPC9zdmc+DQo=
section:
  - name: Show changes
    commands:
      Unstaged changes: git diff
      Staged changes: git diff --staged
      Both (unstaged and staged) changes: git diff HEAD
  - name: History
    commands:
      Diff from yesterday: git diff @{yesterday}..HEAD
      Changes of the last six weeks: git diff @{6 weeks ago}..HEAD
  - name: Changes between branches
    commands:
      Summary (filenames and amount of changes): git diff --compact-summary branch..master
    shortcuts:
      Jump to next file: <kbd>n</kbd>
      Jump to previous file: <kbd>N</kbd>
  - name: Single file
    commands:
      Show file at commit hash: git show 24a255c1:src/main.rs
      Show file at absolute date: git show HEAD@{2013-02-25}:src/main.rs
      Show file at relative date: git show HEAD@{3 days ago}:src/main.rs
      For date older than 90 days: git show (git rev-list -1 --before="2024-07-13" HEAD):src/main.rs
      Restore file to previous version at revision: git checkout 24a255c1 -- src/main.rs
---
