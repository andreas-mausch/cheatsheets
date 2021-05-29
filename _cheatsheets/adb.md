---
layout: cheatsheet
tags: android phone backup
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
adb pull -a /sdcard/WhatsApp/
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
