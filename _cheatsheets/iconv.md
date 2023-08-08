---
layout: cheatsheet
tags: encoding charset convert ascii2uni uni2ascii
section:
  - name: Convert
    commands:
      Convert file from ISO-8859-1 to UTF-8: iconv -f ISO-8859-1 -t UTF-8 in.txt -o out.txt
      Replace unicode character escapes (substitutions, like \u00F6 = ö): ascii2uni -a U -q messages.properties > out.properties
---
