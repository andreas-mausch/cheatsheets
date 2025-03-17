---
layout: cheatsheet
tags: onetime password andotp aegis 2fa oathtool totp-cli
section:
  - name: Calculate code from secret
    commands:
      via oathtool: oathtool --base32 --totp JBSWY3DPEHPK3PXP
  - name: totp-cli
    commands:
      add secret: totp add testprovider
      show code: totp testprovider
---
