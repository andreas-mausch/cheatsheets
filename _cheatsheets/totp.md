---
layout: cheatsheet
tags: onetime password andotp aegis 2fa oathtool totp-cli
section:
  - name: oathtool
    commands:
      Calculate code from secret: oathtool --base32 --totp JBSWY3DPEHPK3PXP --verbose
      read secret from stdin: oathtool --base32 --totp --verbose -
  - name: totp-cli
    commands:
      add secret: totp add testprovider
      show code: totp testprovider
---
