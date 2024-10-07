---
layout: cheatsheet
tags: pacman manjaro aur yay pkgbuild
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+Cjxzdmcgd2lkdGg9IjY1cHgiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDY1IDY1IiB2ZXJzaW9uPSIxLjEiIGhlaWdodD0iNjVweCI+CiA8ZGVmcz4KICA8bGluZWFyR3JhZGllbnQgaWQ9ImxnIiB5MT0iMjYuOTI0JSIgeDI9IjI4LjEyOSUiIHgxPSI1NC42MzglIiB5Mj0iNzkuNTE5JSI+CiAgIDxzdG9wIHN0b3AtY29sb3I9IiNmZmYiIHN0b3Atb3BhY2l0eT0iMCIgb2Zmc2V0PSIwIi8+CiAgIDxzdG9wIHN0b3AtY29sb3I9IiNmZmYiIHN0b3Atb3BhY2l0eT0iLjI3NDUxIiBvZmZzZXQ9IjEiLz4KICA8L2xpbmVhckdyYWRpZW50PgogPC9kZWZzPgogPHBhdGggZD0ibTMyLjI1MyAwLjIwOTkxYy0yLjg0OSA2Ljk4NDMtNC41NzkgMTEuNTU5LTcuNzUgMTguMzM2IDEuOTQ0IDIuMDYxIDQuMzM0IDQuNDUzIDguMjExIDcuMTY0LTQuMTY4LTEuNzE1LTcuMDA5LTMuNDMyLTkuMTMzLTUuMjE5LTQuMDU5IDguNDctMTAuNDIzIDIwLjUzMS0yMy4zMjggNDMuNzE5IDEwLjE0LTUuODU0IDE4LjAwMi05LjQ2NiAyNS4zMjgtMTAuODQ0LTAuMzE0LTEuMzUxLTAuNDgxLTIuODE5LTAuNDY5LTQuMzQ0bDAuMDA4LTAuMzJjMC4xNjEtNi40OTggMy41NDItMTEuNDk1IDcuNTQ3LTExLjE1NiA0LjAwNCAwLjMzOSA3LjEyMiA1Ljg4NCA2Ljk2MSAxMi4zODMtMC4wMzEgMS4yMjQtMC4xNzMgMi40LTAuNDE0IDMuNDkyIDcuMjQ3IDEuNDE4IDE1LjAzNCA1LjAxMyAyNS4wMzkgMTAuNzg5LTEuOTczLTMuNjMyLTMuNzQtNi45MDUtNS40MjItMTAuMDI0LTIuNjQ5LTIuMDUzLTUuNDExLTQuNzI0LTExLjA0Ny03LjYxNyAzLjg3NCAxLjAwNyA2LjY1IDIuMTcxIDguODEyIDMuNDY5LTE3LjA5OC0zMS44MzUtMTguNDgtMzYuMDY4LTI0LjM0My00OS44Mjh2LTAuMDAwMDl6IiBmaWxsPSIjMTc5M0QxIi8+CiA8cGF0aCBpZD0icGF0aDI1MjIiIGZpbGwtb3BhY2l0eT0iLjE2NTY4IiBmaWxsPSIjZmZmIiBkPSJtNTAuMjY2IDM4LjI0OWMtMTMuODcyLTE4LjgyNy0xNy4wODctMzQuMDAyLTE3LjkwMi0zNy42MjUgNy40IDE3LjA2NyA3LjM0OSAxNy4yNzcgMTcuOTAyIDM3LjYyNXoiLz4KIDxwYXRoIGQ9Im0zMi4zNzggMC40NTk5MmMtMC4zNiAwLjg4NDQ4LTAuNyAxLjc0NjgtMS4wMzIgMi41NjI1LTAuMzY0IDAuODk0Ni0wLjcxOCAxLjc1NjUtMS4wNjIgMi41OTM4cy0wLjY5MyAxLjYzMDktMS4wMzEgMi40Mzc1Yy0wLjMzOSAwLjgwNjUtMC42NTQgMS42MDM5LTEgMi40MDYzLTAuMzQ2IDAuODAyLTAuNzI2IDEuNjEzLTEuMDk0IDIuNDM3LTAuMzY4IDAuODI1LTAuNzUyIDEuNjU4LTEuMTU2IDIuNTMyLTAuNDA0IDAuODczLTAuODI4IDEuODAxLTEuMjgyIDIuNzUtMC4wNjEgMC4xMjgtMC4xMjQgMC4yNzYtMC4xODcgMC40MDYgMS45MzkgMi4wNTQgNC4zMyA0LjQyNyA4LjE4NyA3LjEyNS00LjE2Ny0xLjcxNS03LTMuNDMyLTkuMTI1LTUuMjE5LTAuMTEgMC4yMjYtMC4xOTggMC40MjUtMC4zMTIgMC42NTYtMC40MiAwLjg3MS0wLjg3MSAxLjczMy0xLjM0NCAyLjY4OC0wLjExMyAwLjIyNC0wLjE5NiAwLjQyNy0wLjMxMiAwLjY1Ni0wLjUwMSAxLjAwNC0xLjAyNiAyLjA0My0xLjU5NCAzLjE1Ni0wLjExMyAwLjIyLTAuMjI4IDAuNDAyLTAuMzQ0IDAuNjI1LTAuMzQzIDAuNjY3LTEuNDQgMi43Ny0yLjU2MiA0LjkwNy0wLjY1NSAxLjI0OC0xLjE2OSAyLjI3LTEuOTA3IDMuNjU2LTAuMjA5IDAuMzk4LTAuNjM5IDEuMTk1LTAuNzUgMS40MDYgOC4xMjUtNC41NzMgMTYuODkxLTExLjIxNiAzMi44MTMtNS41MzEtMC43OTctMS41MS0xLjU2Mi0yLjkxOS0yLjI1LTQuMjUtMC42ODgtMS4zMzItMS4zMTItMi41NzEtMS45MDYtMy43NXMtMS4xNDMtMi4yOTEtMS42NTctMy4zNDRjLTAuNTEzLTEuMDUzLTAuOTg5LTIuMDQ3LTEuNDM3LTNzLTAuODg1LTEuODctMS4yODEtMi43NWMtMC4zOTctMC44NzktMC43NjYtMS43My0xLjEyNS0yLjU2Mi0wLjM1OS0wLjgzMy0wLjY5NS0xLjY1OC0xLjAzMi0yLjQ2OS0wLjMzNi0wLjgxMTUtMC42NzItMS41ODk2LTEtMi40MDYzLTAuMTQyLTAuMzU1NC0wLjI2My0wLjczMzgtMC40MDYtMS4wOTM4LTAuODg4LTIuMDg0OS0xLjc1OS00LjE1MTUtMi44MTItNi42MjV2MC4wMDAwMnoiIGZpbGw9InVybCgjbGcpIi8+Cjwvc3ZnPgo=
section:
  - name: Install
    commands:
      install: paru -S <package>
      Edit PKGBUILD and skip checksum check: paru -S gnucash-xbt --fm helix --mflags "--skipchecksums"
      "uninstall (-n: no backup files; -s: remove dependencies)": paru -Rns <package>
      system update: paru -Syu
  - name: Mirrors
    commands:
      select fastest: sudo pacman-mirrors --fasttrack
      select by country: sudo pacman-mirrors --country Germany,France,Austria
  - name: Search repo
    commands:
      search package: paru -Ss <package>
      package details: paru -Si <package>
      list files: paru -Fl <package>
      find package for file: pkgfile <filename>
      search command: paru -F glxinfo # will output extra/mesa-utils
  - name: Installed packages
    commands:
      - title: search package
        command: paru -Qs <package>
      - title: package details
        command: paru -Qii <package>
      - title: list files
        command: paru -Ql <package>
      - title: orphans
        command: paru -Qdt
      - title: manually installed (list all aur)
        command: pacman -Qm
      - title: manually installed (aur and non-aur)
        command: pacman -Qqe | grep -v "$(awk '{print $1}' /desktopfs-pkgs.txt)"
        source: https://www.reddit.com/r/ManjaroLinux/comments/fzog8g/get_a_list_of_packages_you_installed_yourself/
        options:
          -Q: "--query: Query the package database"
          -q: --quiet
          -e: "--explicit: Restrict or filter output to explicitly installed packages"
  - name: Clean-up
    commands:
      clear cache: paru -Sc
  - name: Official repo vs. AUR
    commands:
      repo: paru -[...] --repo
      aur: paru -[...] --aur
---
