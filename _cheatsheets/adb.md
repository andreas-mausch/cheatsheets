---
layout: cheatsheet
tags: android phone backup
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2aWV3Qm94PSItMTQ3IC03MCAyOTQgMzQ1Ij4KPGcgZmlsbD0iI2E0YzYzOSI+Cjx1c2Ugc3Ryb2tlLXdpZHRoPSIxNC40IiB4bGluazpocmVmPSIjYiIgc3Ryb2tlPSIjRkZGIi8+Cjx1c2UgeGxpbms6aHJlZj0iI2EiIHRyYW5zZm9ybT0ic2NhbGUoLTEsMSkiLz4KPGcgaWQ9ImEiIHN0cm9rZT0iI0ZGRiIgc3Ryb2tlLXdpZHRoPSI3LjIiPgo8cmVjdCByeD0iNi41IiB0cmFuc2Zvcm09InJvdGF0ZSgyOSkiIGhlaWdodD0iODYiIHdpZHRoPSIxMyIgeT0iLTg2IiB4PSIxNCIvPgo8cmVjdCBpZD0iYyIgcng9IjI0IiBoZWlnaHQ9IjEzMyIgd2lkdGg9IjQ4IiB5PSI0MSIgeD0iLTE0MyIvPgo8dXNlIHk9Ijk3IiB4PSI4NSIgeGxpbms6aHJlZj0iI2MiLz4KPC9nPgo8ZyBpZD0iYiI+CjxlbGxpcHNlIGN5PSI0MSIgcng9IjkxIiByeT0iODQiLz4KPHJlY3Qgcng9IjIyIiBoZWlnaHQ9IjE4MiIgd2lkdGg9IjE4MiIgeT0iMjAiIHg9Ii05MSIvPgo8L2c+CjwvZz4KPGcgc3Ryb2tlPSIjRkZGIiBzdHJva2Utd2lkdGg9IjcuMiIgZmlsbD0iI0ZGRiI+CjxwYXRoIGQ9Im0tOTUgNDQuNWgxOTAiLz48Y2lyY2xlIGN4PSItNDIiIHI9IjQiLz48Y2lyY2xlIGN4PSI0MiIgcj0iNCIvPgo8L2c+Cjwvc3ZnPg==
---

# Phone backup

## Copy files from phone

```
adb pull -a /sdcard/DCIM/Camera/
adb pull -a /sdcard/DCIM/Screenshots/
adb pull -a /sdcard/Snapseed/
```

### Whatsapp

```
adb pull -a /sdcard/Android/media/com.whatsapp/
cd com.whatsapp
rsync -rltvh0 --stats ./WhatsApp/Media/ "./2013-01-01 WhatsApp Media/Media" --ignore-existing
zip -r0 "2013-01-01 WhatsApp Media.zip" .
```

## Copy files to my external hard drive

```
# Archive (keep timestamp) and don't overwrite existing
sudo cp -an /source/ .
```

```
# All files belong to root, so I cannot delete files by mistakes that easily
sudo chown -R root:root .
sudo chmod -R 644 *
sudo chmod -R +X *
```

## rsync

Update folder:
```
rsync -avh0 --stats ./source/ ./target/
```

Notes:
- [Command line options](https://explainshell.com/explain?cmd=rsync+-avh0+--stats+.%2Fsource%2F+.%2Ftarget%2F)
  - -a: archive mode; equals -rlptgoD
  - -v: increase verbosity
  - -h: output numbers in a human-readable format
  - -0: terminated by a null ('\0') character, not a NL, CR, or CR+LF
  - --stats: This tells rsync to print a verbose set of statistics on the file transfer
- Use "rlt" (recursive, symlinks and preserve timestamps) instead of "a" if you don't want to display directories with different owner/permissions
- Use "n" for dry run
- You might use "--ignore-existing" or "--ignore-non-existing"

## Reduce size of pictures

### Resize images in *Andere* folder

```
magick mogrify -resize "3840x3840>" -quality 75 -define preserve-timestamp=true ./Andere/*.JPG
```

### Resize all images >1.5mb

```
find *.jpg -type f -size +1500k -exec magick mogrify [...] {} \;
```

### Combined

```
find ./Andere/ \( -iname "*.jpg" -o -iname "*.jpeg" \) -type f -size +1500k -exec magick mogrify -resize "3840x3840>" -quality 75 -define preserve-timestamp=true {} \;
```
