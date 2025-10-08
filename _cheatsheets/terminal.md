---
layout: cheatsheet
tags: shell bash ansi colors rtf html
section:
  - name: Copy colored terminal output
    commands:
      Copy in RTF format: curl -fsSL https://raw.githubusercontent.com/Neved4/color.sh/refs/tags/v0.1.0/src/color.sh | sh | ansifilter --rtf | xclip -selection clipboard -t text/rtf
      Copy in HTML format: curl -fsSL https://raw.githubusercontent.com/Neved4/color.sh/refs/tags/v0.1.0/src/color.sh | sh | ansifilter --html | xclip -selection clipboard -t text/html
      Alternative using aha: curl -fsSL https://raw.githubusercontent.com/Neved4/color.sh/refs/tags/v0.1.0/src/color.sh | sh | aha | xclip -selection clipboard -t text/html
---
