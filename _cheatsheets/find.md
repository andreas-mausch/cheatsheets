---
layout: cheatsheet
tags: filetypes files search duplicates same fdupes chmod
section:
  - name: File types
    commands:
      Find file types in directory: find . -type f | perl -ne 'print $1 if m/\.([^.\/]+)$/' | sort -ub
      List file count and sizes grouped by extension: find . -name '?*.*' -type f -print0 | perl -0ne 'if (@s = stat$_){ ($ext = $_) =~ s/.*\.//s; $s{$ext} += $s[12]; $n{$ext}++; } END { for (sort{$s{$a} <=> $s{$b}} keys %s) { printf "%15d %6d %s\n",  $s{$_}<<9, $n{$_}, $_; } }' | numfmt --to=iec-i --suffix=B
      Largest files: find . -type f -exec du -Sh {} + | sort -rh | head -n 10
  - name: Clean up
    commands:
      Delete node_modules recursively: find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +
  - name: Search for duplicates in two directories
    commands:
      Sorted by filename: fdupes --recurse --size --time --order=name ./folder1/ ./folder2/ > fdupes-sort-by-name.txt
  - name: File permissions
    commands:
      Show linux file permissions in numeric format (e.g. 755): find . -maxdepth 1 -printf "%m %f\n"
  - name: Last change
    commands:
      Show all files changed within the last year: find . -ctime 365 2>/dev/null
  - name: Filter by pattern
    commands:
      Show only folders containing at least one file matching a pattern: find . -iname "dsc_*" -printf "%h\n" | sort -u
  - name: Find string in files
    commands:
      grep: grep -iRs --exclude-dir=node_modules --exclude-dir=dist --exclude-dir=build --exclude-dir=.git --exclude=package-lock.json "string" .
---
