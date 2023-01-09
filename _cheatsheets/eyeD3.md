---
layout: cheatsheet
tags: music mp3 id3v2 cover
section:
  - name: Show
    commands:
      List tags for file: eyeD3 song.mp3
      Extract cover: eyeD3 --write-images=. song.mp3
  - name: Change
    commands:
      Rename mp3 file based on id3 tags using eyeD3: eyeD3 --rename '$album_artist - $album - $track:num - $title' *.mp3
      Set artist and composer: eyeD3 --artist=Artist --album-artist=Artist --composer=Artist song.mp3
      Set track and total number of tracks: eyeD3 --track=3 --track-total=12 song.mp3
      Set disc and total number of discs: eyeD3 --disc-num=1 --disc-total=2 song.mp3
      Release year: eyeD3 --release-year=2023 song.mp3
      Genre: eyeD3 --genre=Rap song.mp3
  - name: Fixup
    commands:
      Show inconsistencies: eyeD3 --plugin=fixup --dry-run --type=lp --file-rename-pattern='$album_artist - $album - $track:num - $title' --dir-rename-pattern='$album_artist - $album ($release_date:year)' .
      Cleanup: eyeD3 --to-v2.3 --remove-v1 --remove-all-comments --remove-all-lyrics --remove-all-images --remove-all-objects --user-text-frame='ARTISTS:' --user-text-frame='eyeD3#album_type:' *.mp3
---

Typical workflow:

```bash
eyeD3 --plugin=fixup --type=lp --file-rename-pattern='$album_artist - $album - $track:num - $title' --dir-rename-pattern='$album_artist - $album ($release_date:year)' .
eyeD3 --to-v2.3 --remove-v1 --remove-all-comments --remove-all-lyrics --remove-all-images --remove-all-objects --user-text-frame='ARTISTS:' --user-text-frame='eyeD3#album_type:' *.mp3
eyeD3 --disc-num=1 --disc-total=1 *.mp3
eyeD3 --genre=Rap *.mp3
eyeD3 --add-image='cover.jpg:FRONT_COVER' *.mp3
```
