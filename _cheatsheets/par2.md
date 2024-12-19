---
layout: cheatsheet
tags: archive recovery parity parchive
section:
  - name: Create
    commands:
      - title: Index + Single file parity data
        command: par2 create -m2048 -v -r5 -n1 output.par2 input.bin
        options:
          -m: Maximum Memory usage in Megabytes
          -v: Enable verbose mode
          -r: Recovery data in percent
          -n: Number of parity files to create
  - name: Verify
    commands:
      - title: Verify
        command: par2 verify -m2048 -v input.par2
        options:
          -m: Maximum Memory usage in Megabytes
          -v: Enable verbose mode
---

> As stated in the documentation, the -n option controls the number of parity files created and has no effect on the amount of parity data created nor the amount of damage it can repair. Keep in mind that parchive was originally created for usenet/news downloads where the structure of the parity files meant less damaged files could be repaired by smaller parity files, which also had to be downloaded. In other words, it was desirable not to have to download all the available parity information to repair a file with minor damage. However, this nesting has no real benefit where the files and parity data are available locally so generating multiple, nested parity files makes no sense. In that case, the only reason to create more than 1 parity file is if the amount of parity data itself is too large.
> -- <https://superuser.com/questions/1116826/how-to-parchive>
