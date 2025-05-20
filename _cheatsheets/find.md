---
layout: cheatsheet
tags: filetypes files search duplicates same fdupes chmod touch xargs fd
section:
  - name: File types
    commands:
      Find file types in directory: find . -type f | perl -ne 'print $1 if m/\.([^.\/]+)$/' | sort -ub
      List file count and sizes grouped by extension: find . -name '?*.*' -type f -print0 | perl -0ne 'if (@s = stat$_){ ($ext = $_) =~ s/.*\.//s; $s{$ext} += $s[12]; $n{$ext}++; } END { for (sort{$s{$a} <=> $s{$b}} keys %s) { printf "%15d %6d %s\n",  $s{$_}<<9, $n{$_}, $_; } }' | numfmt --to=iec-i --suffix=B
      Largest files: find . -type f -exec du -Sh {} + | sort -rh | head -n 10
  - name: Clean up
    commands:
      Delete all files matching a pattern recursively (remove the echo): find . -type f -name '*.log' -print0 | xargs --null [--max-args=1] echo rm --verbose
      Delete node_modules recursively: find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +
  - name: Search for duplicates in two directories
    commands:
      Sorted by filename: fdupes --recurse --size --time --order=name ./folder1/ ./folder2/ > fdupes-sort-by-name.txt
  - name: File permissions
    commands:
      Show linux file permissions in numeric format (e.g. 755): find . -maxdepth 1 -printf "%m %f\n"
  - name: Last change
    commands:
      All files changed in the last 3 minutes in your home: find ~ -mmin -3 -ls
      Show all files changed within the last year: find . -ctime -365
      Show all files which are older than one year: find . -ctime +365
      Create an old file for testing: touch -mt 200501011400 old_file
      Use mtime instead of ctime: find . -mtime -365
  - name: Filter by pattern
    commands:
      Show only folders containing at least one file matching a pattern: find . -iname "dsc_*" -printf "%h\n" | sort -u
      Run with xargs: find . -type f -name '*.log' -print0 | xargs --null -I{} echo 'File is {}.'
  - name: Find string in files
    commands:
      grep: grep -iRs --exclude-dir=node_modules --exclude-dir=dist --exclude-dir=build --exclude-dir=.git --exclude=package-lock.json "string" .
---

Scratch all of the above and use [fd](https://github.com/sharkdp/fd),
a simple, fast and user-friendly alternative to 'find'.
