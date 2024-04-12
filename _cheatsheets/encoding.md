---
layout: cheatsheet
tags: base16 base32 base64 utf-8 unicode
section:
  - name: Base32
    commands:
      Encode: echo -n 'my-string' | base32 --wrap=0
      Decode: echo -n 'NV4S243UOJUW4ZY=' | base32 --decode
      Decode ignoring padding: echo -n 'NV4S243UOJUW4ZY'==== | fold -w 4 | head -n -1 | tr --delete '\n' | base32 --decode
  - name: Base64
    commands:
      Encode: echo -n 'my-string' | base64 --wrap=0
      Decode: echo -n 'bXktc3RyaW5n' | base64 --decode
      Decode ignoring padding: echo -n 'aGVsbG8td29ybGQ'==== | fold -w 4 | head -n -1 | tr --delete '\n' | base64 --decode
---

Base16 / String to hex: See xxd

UTF-8 / Unicode / ISO-8859-1 / ASCII: See iconv
