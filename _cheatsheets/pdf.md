---
layout: cheatsheet
tags: ghostscript enscript
section:
  - name: Generation
    commands:
      Generate PDF from string: gs -dBATCH -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=test.pdf (echo -e "@color{0.5 0 0} @font{Courier-Bold36} \n\n\n foo" | enscript --no-header -e@ -p - | psub)
---
