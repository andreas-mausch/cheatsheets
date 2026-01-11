---
layout: cheatsheet
tags: ghostscript enscript
section:
  - name: Generation
    commands:
      Generate PDF from string: gs -dBATCH -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=test.pdf (echo -e "@color{0.5 0 0} @font{Courier-Bold36} \n\n\n foo" | enscript --no-header -e@ -p - | psub)
      Generate PDF from .png images with OCR text recognition: img2pdf *.png | ocrmypdf --rotate-pages --rotate-pages-threshold=10.0 --language deu+eng - out.pdf
  - name: Optimization
    commands:
      Reduce file size: gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dDownsampleColorImages=true -dColorImageResolution=120 -dGrayImageResolution=120 -dMonoImageResolution=150 -dJPEGQ=65 -dNOPAUSE -dBATCH -sOutputFile=output.pdf input.pdf
  - name: Decryption
    commands:
      Remove password from protected .pdf file: qpdf --decrypt protected.pdf --password=<your-password> out.pdf
      Pass password via stdin: qpdf --decrypt protected.pdf --password-file=- out.pdf
---

# Notes on passing the password

[Allow Password Input From Standard Input for Increased Security #1188 - github.com](https://github.com/qpdf/qpdf/issues/1188)

> Reads the first line from the specified file and uses it as the password for accessing encrypted files. filename may be - to read the password from standard input, but if you do that the password is echoed and there is no prompt, so use - with caution. Note that leading and trailing spaces are not stripped from the password.
> -- <https://qpdf.readthedocs.io/en/stable/cli.html#general-options>

Press enter, then **CTRL+D** after entering the password.
