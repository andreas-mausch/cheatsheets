---
layout: cheatsheet
tags: backup copy
section:
  - name: Copy directory and preserve as much info as possible
    commands:
      - title: Copy (archive)
        command: sudo rsync -avAXh --info=progress2 --info=name0 /mnt/source/ /mnt/target/
        options:
          -a: "--archive: equals -rlptgoD (no -H,-A,-X)"
          -v: "--verbose"
          -A: "--acls: preserve ACLs (implies -p)"
          -X: "--xattrs: preserve extended attributes"
          -h: "--human-readable"
          "--info=progress2": Best way to show total progress
          "--info=name0": Hide filenames for cleaner output
          -r: "--recursive"
          -l: "--links: copy symlinks as symlinks"
          -p: "--perms: preserve permissions"
          -t: "--times: preserve modification times"
          -g: "--group: preserve group"
          -o: "--owner: preserve owner (super-user only)"
          -D: "same as --devices --specials"
          --devices: preserve device files (super-user only)
          --specials: preserve special files
      - title: Copy as the current user
        command: sudo rsync -rltvXh --info=progress2 --info=name0 /mnt/source/ /mnt/target/
---

# Optional extra arguments

- `-n`: `--dry-run`
- `-i`: `--itemize-changes`
- `-z`: `--compress`
- `-P`: `--partial` (continues files)
- `-H`: `--hard-links` (preserve hard links)
- `--ignore-existing` / `--ignore-non-existing` (= `--existing`)

# Itemize Changes

<https://stackoverflow.com/questions/4493525/what-does-f-mean-in-rsync-logs>

<https://dev.to/alexisayenko/understanding-rsync-itemize-changes-5fgi>

The log output can be interpreted like this:

## >f.st......

```
> - the item is received
f - it is a regular file
s - the file size is different
t - the time stamp is different
```

## .d..t......

```
. - the item is not being updated (though it might have attributes
    that are being modified)
d - it is a directory
t - the time stamp is different
```

## >f+++++++++

```
> - the item is received
f - a regular file
+++++++++ - this is a newly created item
```

# For copying system drives

## Replicate partition table

Recreate all partitions manually.

## Mount both drives (old and new) and copy files

Use rsync to copy files.

Note:

> for system drives, copying /dev, /proc, /sys directories should be avoided:
> either exclude them with --exclude or do this from a live environment.
>
> --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","lost+found"}

## Reinstall GRUB

```bash
sudo mount --bind /dev /mnt/target/dev
sudo mount --bind /proc /mnt/target/proc
sudo mount --bind /sys /mnt/target/sys
sudo chroot /mnt/target
grub-install /dev/sdY
update-grub
```

## Update /etc/fstab if needed

1. Check `sudo blkid` to see new UUIDs.
2. Edit `/mnt/target/etc/fstab` to match the new partition UUIDs so it boots correctly.
