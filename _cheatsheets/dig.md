---
layout: cheatsheet
tags: domain reverse lookup
section:
  - name: DNS lookup
    commands:
      Get IP for domain name: dig google.com
      Get domain name for IP (reverse lookup): dig -x 157.240.210.35
      Shorten output: dig -x 157.240.210.35 +short
      Get A records: dig google.com +noall +answer -t A
      Get AAAA records: dig google.com +noall +answer -t AAAA
---
