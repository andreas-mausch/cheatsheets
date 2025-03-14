---
layout: cheatsheet
tags: svg-term-cli record cast terminal
logo: data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxMDAwIDEwMDAiPjxkZWZzPjxtYXNrIGlkPSJhIj48cmVjdCB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiBmaWxsPSIjZmZmIi8+PHBhdGggZD0iTTcwMCA1MDAgNDAwIDMyNi43OTV2MzQ2LjQxeiIvPjwvbWFzaz48L2RlZnM+PHBhdGggZmlsbD0iI2Q0MDAwMCIgZD0iTTEwMDAgNTAwIDI1MCA2Ni45ODd2ODY2LjAyNnoiIG1hc2s9InVybCgjYSkiLz48cGF0aCBzdHJva2U9IiNkNDAwMDAiIHN0cm9rZS13aWR0aD0iOTAiIGQ9Im02NzMuMjA1IDQwMC0zNDYuNDEgMjAwIi8+PC9zdmc+
section:
  - name: Create cast
    commands:
      Record: asciinema rec ./recording.cast
      Record as 80x24: xfce4-terminal --geometry=80x24 --command="asciinema rec ./recording.cast"
      Also hide suggestions: xfce4-terminal --geometry=80x24 --command="asciinema rec ./recording.cast --command='/usr/bin/fish --private --init-command=\"function fish_greeting; end\"'"
      Convert to SVG: svg-term --in recording.cast --out recording.svg
---
