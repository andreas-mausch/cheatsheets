---
layout: cheatsheet
tags: document paper ocr
logo: data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMCIgaGVpZ2h0PSIyMCI+PHBhdGggZmlsbD0iIzY2NiIgZD0iTTEwLjc3MyA4LjMxOCAxIDEzLjg5djEuOTQ3bDkuMTY3IDMuMDgxTDE5IDExLjYwNVY5Ljg5M2wtNS40ODQtOC4wMjQtNy43MTItLjc4Ni0uNDM2LjQzNXoiLz48cGF0aCBmaWxsPSIjZmZmIiBkPSJtMTEuMTQ3IDguMjgxLTkuOTExIDUuNjg2djEuNzFsOC44MzcgMi45MzUgOC41ODktNy4xNTdWOS43MzR6Ii8+PHBhdGggZmlsbD0iI2I1YjViNSIgZD0ibTE4LjMzOCA5Ljg5Ni4yNDQtLjE2MiIvPjxwYXRoIGZpbGw9IiNlYWVhZWUiIGQ9Im0xMS4yMTMgOC4yNDQtLjEzMi4wNzUtOS44NDUgNS42NDkgOC44MzggMi45MjMgOC41ODgtNy4xNTd6Ii8+PHBhdGggZmlsbD0iIzAzMjFjMyIgZD0ibTEwLjMzNyAxNS43MzggNi44ODEtNS43MzQtNS44MTQtMS4yMTMtOC4wOTQgNC42ODR6Ii8+PHBhdGggZmlsbD0iIzUyYTRmOSIgZD0ibTEwLjMwMiAxNS42MTIgNi42NTItNS41NDQtNS41MTUtMS4xNS03Ljg2MSA0LjUzN3oiLz48cGF0aCBmaWxsPSIjZWFlYWVlIiBkPSJNOS45MDcgMTguNTUxdi0xLjU1bC04LjY3LTIuODY4djEuNTU1eiIvPjxwYXRoIGZpbGw9IiNkN2Q3ZTIiIGQ9Ik00LjQzNyAxNS4xOTJhLjYuNiAwIDAgMC0uMDI1LjIwMWMuMDUyLjUxNi44ODUuODU1IDEuODYxLjc1Ny4yMjMtLjAyMi40MzUtLjA4NC42MjctLjE0M3oiLz48cGF0aCBmaWxsPSIjZWFlYWVlIiBkPSJNMTAuMjMgMTYuOTI2djEuNTU1bDguNDMyLTcuMDI3VjkuOXoiLz48cGF0aCBmaWxsPSJ1cmwoI2MpIiBkPSJtMTAuOTcxIDguNDA2IDcuNDQ5IDEuNDkiLz48cGF0aCBmaWxsPSIjZWNlY2VlIiBkPSJtNS41NjkgMS42MSA1LjQxOCA2LjggNy40MyAxLjUyNy4yNDUtLjIwMy01LjI2Ny03LjcwNy03LjQ2OC0uNzc0eiIvPjxwYXRoIGZpbGw9IiNkMWQxZDgiIGQ9Im0xOC40MTggOS45MzctNy40NS0xLjU1My01LjQtNi43NzMgNy41NTQuNzd6Ii8+PC9zdmc+
section:
  - name: Scan document
    commands:
      - title: Scan A4 document to .jpg (1920x1080 pixels)
        command: scanimage --device-name 'hpaio:/usb/OfficeJet_Pro_6000?serial=TH12345678' --progress --format tiff --mode Color --resolution 300 -l 0mm -t 0mm -x 210mm -y 297mm | magick - -resize '1920x1920>' -quality 75 out.jpg
      - title: Scan A4 document to .png (lossless)
        command: scanimage --device-name 'hpaio:/usb/OfficeJet_Pro_6970?serial=TH12345678' --progress --format tiff --mode Color --resolution 300 -l 0mm -t 0mm -x 210mm -y 297mm | magick - 1.png
      - title: Combine multiple pngs to a single .pdf and add OCR
        command: img2pdf *.png | ocrmypdf --language deu+eng - out.pdf
---
