---
layout: cheatsheet
tags: key derivation function hkdf pbkdf2 bip39 argon2
section:
  - name: openssl
    commands:
      List supported algorithms: openssl list -kdf-algorithms
      HKDF: openssl kdf [-binary] -keylen 10 -kdfopt digest:SHA2-256 -kdfopt key:secret [-kdfopt salt:salt] -kdfopt info:label HKDF
      Argon2: openssl kdf -keylen 16 -kdfopt pass:secret -kdfopt salt:saltsalt -kdfopt iter:2048 -kdfopt memcost:8 Argon2id
      PBKDF2: openssl kdf -keylen 64 -kdfopt digest:sha512 -kdfopt iter:2048 -kdfopt pass:'abandon abandon abandon abandon abandon abandon abandon abandon abandon abandon abandon about' -kdfopt salt:'mnemonicMYPASSPHRASE' pbkdf2
---

The salt in HKDF is optional, see [here](https://crypto.stackexchange.com/questions/97975/applications-in-which-you-should-shouldnt-use-a-salt-with-hkdf).

# Which algorithm to use?

From ChatGPT:

> If you're:
> - Deriving from a secure key (like your GPG private key): use HKDF
> - Using a password or passphrase: use PBKDF2 (or even better: Argon2)
> - Working under FIPS/NIST or enterprise compliance: use SSKDF

# Argon2: i vs. d vs. id

From ChatGPT:

> TL;DR — Which one should you use?
> ✅ Use Argon2id in almost all cases.
> It’s the most secure and recommended hybrid — combining the best of both i and d.
