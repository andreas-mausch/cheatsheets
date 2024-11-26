---
layout: cheatsheet
tags: power
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/Pgo8c3ZnIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDY0IDY0Ij48ZGVmcz48bGluZWFyR3JhZGllbnQgaWQ9IjAiIHgxPSI3NzMuMDgiIHkxPSIyMjAuMTIiIHgyPSI3NzMuMzIiIHkyPSIxNzkuODciIGdyYWRpZW50VW5pdHM9InVzZXJTcGFjZU9uVXNlIj48c3RvcCBzdG9wLWNvbG9yPSIjNDliOTAzIi8+PHN0b3Agb2Zmc2V0PSIxIiBzdG9wLWNvbG9yPSIjOGNmZjA3Ii8+PC9saW5lYXJHcmFkaWVudD48bGluZWFyR3JhZGllbnQgaWQ9IjEiIHgxPSI3NzIuNDkiIHkxPSIyMjEuODciIHgyPSI3NzIuNDUiIHkyPSIxNjMuODMiIGdyYWRpZW50VW5pdHM9InVzZXJTcGFjZU9uVXNlIj48c3RvcCBzdG9wLWNvbG9yPSIjMTQxNDE0Ii8+PHN0b3Agb2Zmc2V0PSIxIiBzdG9wLWNvbG9yPSIjMmQyZDJmIi8+PC9saW5lYXJHcmFkaWVudD48L2RlZnM+PGcgdHJhbnNmb3JtPSJtYXRyaXgoLjkyODU3IDAgMCAuOTI4NTctNjg1LjI5LTE0Ni4xKSI+PHBhdGggZD0ibTc5Mi41NyAyMTguMzdjMCAuNzkzLS43NjUgMS40MzYtMS41NTggMS40MzZoLTM3LjMzYy0uNzkzIDAtMS4zMTQtLjY0My0xLjMxNC0xLjQzNnYtMzguNzY5aDQwLjIxdjM4Ljc2OSIgZmlsbD0idXJsKCMwKSIvPjxwYXRoIGQ9Im03OTIuNTcgMTc5LjZ2LTguNjE1YzAtLjc5My0uNzgtMS40MzYtMS41NzItMS40MzZoLTkuOTE1di00LjMwOGMwLS43OTMtLjc4LTEuNDM2LTEuNTcyLTEuNDM2aC0xNC4zNTljLS43OTMgMC0xLjI5OS42NDMtMS4yOTkgMS40MzZ2NC4zMDhoLTEwLjE4OGMtLjc5MyAwLTEuMjk5LjY0My0xLjI5OSAxLjQzNnY4LjYxNWg0MC4yMSIgZmlsbD0idXJsKCMxKSIvPjxwYXRoIGQ9Im03NzUuNTkgMTc5LjU1bC0xMi40NjggMTUuMTY3IDguNDEzIDQuNTUyLTIuMTc5IDEwLjYxNSAxMi40NjgtMTUuMTY3LTguNDEzLTQuNTUyeiIgZmlsbD0iI2ZmZiIgZmlsbC1vcGFjaXR5PSIuOTIiLz48L2c+PC9zdmc+
section:
  - name: Info
    commands:
      Manufacture date and serial number: sudo dmidecode -t 22
      Show cycle count: cat /sys/class/power_supply/BAT0/cycle_count
  - name: Capacity
      Original (design) capacity: cat /sys/class/power_supply/BAT0/energy_full_design
      Remaining capacity on full charge: /sys/class/power_supply/BAT0/energy_full
      acpi: acpi -V
---