---
layout: cheatsheet
tags: image-processing webp
section:
  - name: Image modification
    commands:
      Downscale: "magick mogrify -auto-orient -strip -resize \"1920x1920>\" -quality 85 *.jpg"
      Convert to webp: "magick convert -auto-orient -strip -resize \"600x600>\" -quality 75 -define webp:method=6 -define webp:use-sharp-yuv=1 image.jpg image.webp"
      Batch processing: "for i in *.jpg; do magick convert /* your options */ $i ${i/.jpg/.webp}; done"
      Preserve timestamp: "magick mogrify -define preserve-timestamp=true <filename.jpg>"
      Iterate big files: "find . \\( -iname \"*.jpg\" -o -iname \"*.jpeg\" \\) -type f -size +1500k -exec magick mogrify [...] {} \\;"
  - name: Image information
    commands:
      Quality of jpeg: "magick identify -format '%Q' <filename.jpg>"
---
