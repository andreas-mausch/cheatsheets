---
layout: cheatsheet
tags: key derivation function hkdf
section:
  - name: openssl
    commands:
      HKDF: openssl kdf [-binary] -keylen 10 -kdfopt digest:SHA2-256 -kdfopt key:secret [-kdfopt salt:salt] -kdfopt info:label HKDF
---

The salt in HKDF is optional, see [here](https://crypto.stackexchange.com/questions/97975/applications-in-which-you-should-shouldnt-use-a-salt-with-hkdf).
