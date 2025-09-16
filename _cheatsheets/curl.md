---
layout: cheatsheet
tags: nghttp http2 http3 ssl tls certificates load-testing rate-limit
section:
  - name: curl
    commands:
      Show http version with curl: curl -sI https://curl.se -o/dev/null -w '%{http_version}\n'
      Enable http3 support: curl -sI --http3 https://curl.se -o/dev/null -w '%{http_version}\n'
      Accept TLS server certificate for a different host name and still send a client certificate: curl -v --cert-type P12 --cert certificate.p12:password --resolve host.name:443:192.168.1.123 https://host.name
  - name: nghttp
    commands:
      List resources (s=print stats, a=download assets, n=discard data): "nghttp --stat --get-assets --null-out https://andreas-mausch.de"
---

For load testing, I recommend the tool [oha](https://github.com/hatoo/oha).
