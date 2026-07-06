---
layout: cheatsheet
tags: filetypes files search eza
section:
  - name: File sizes
    commands:
      Largest files: fd -t f -X du -Sh | sort -rh | head -n 10
  - name: Delete files by pattern
    commands:
      Delete files by pattern: fd "pattern" -x echo rm -v --
      Clean up empty directories: fd "pattern" --type empty --type directory --bottom-up -x echo rmdir --
      Clean up macOS dot files (like dot_clean): fd -H '^\._' -x echo rm -v --
  - name: Last change
    commands:
      Show all files changed within the last year: fd --changed-within 1year -X eza --sort=modified
      Show all files which are older than one year: fd --change-older-than 1year -l
---

If a filename starts with a dash (e.g., -somefile.txt),
rm might mistake the filename for a command-line option
and throw an error.
To prevent this, add `--` before the placeholder
to tell `rm` that no more options are coming.
