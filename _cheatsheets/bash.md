---
layout: cheatsheet
tags: terminal shebang
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz48IS0tIFVwbG9hZGVkIHRvOiBTVkcgUmVwbywgd3d3LnN2Z3JlcG8uY29tLCBHZW5lcmF0b3I6IFNWRyBSZXBvIE1peGVyIFRvb2xzIC0tPgo8c3ZnIHdpZHRoPSI4MDBweCIgaGVpZ2h0PSI4MDBweCIgdmlld0JveD0iMCAwIDE2IDE2IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZlcnNpb249IjEuMSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbGluZWNhcD0icm91bmQiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS13aWR0aD0iMS41Ij4NCjxyZWN0IGhlaWdodD0iMTAuNSIgd2lkdGg9IjEyLjUiIHk9IjIuNzUiIHg9IjEuNzUiLz4NCjxwYXRoIGQ9Im04Ljc1IDEwLjI1aDIuNW0tNi41LTQuNSAyLjUgMi4yNS0yLjUgMi4yNSIvPg0KPC9zdmc+
section:
  - name: Shebang
    commands:
      - title: My favorite shebang
        command: '#!/usr/bin/env -S bash -euo pipefail'
        options:
          -S: "--split-string: process and split S into separate arguments; used to pass multiple arguments on shebang lines"
          -e: errexit, exit immediately if a command fails
          -u: nounset, treats unset variables as an error
          -o pipefail: prevents errors in a pipeline from being masked
          -x: Print a trace of simple commands
---

The Set Builtin:

<https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html>

While env -S is standard on modern Linux (GNU coreutils) and macOS,
it is not POSIX-compliant. Older Unix systems or stripped-down busybox
environments may not support -S.
