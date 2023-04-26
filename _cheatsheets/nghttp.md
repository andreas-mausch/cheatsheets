---
layout: cheatsheet
tags: http2 http3
section:
  - name: List resources
    commands:
      s=print stats, a=download assets, n=discard data: "nghttp --stat --get-assets --null-out https://andreas-mausch.de"
  - name: curl
    commands:
      Show http version with curl: curl -sI https://curl.se -o/dev/null -w '%{http_version}\n'
      Enable http3 support: curl -sI --http3 https://curl.se -o/dev/null -w '%{http_version}\n'
---
