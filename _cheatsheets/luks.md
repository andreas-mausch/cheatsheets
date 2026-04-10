---
layout: cheatsheet
tags: encryption boot
section:
  - name: Show
    commands:
      Show information for encrypted partition: sudo cryptsetup luksDump /dev/nvme0n1p2
      Find key slot for passphrase: sudo cryptsetup --verbose open --test-passphrase /dev/nvme0n1p2
  - name: Change
    commands:
      Delete key: sudo cryptsetup --verbose luksKillSlot /dev/nvme0n1p2 N
---

# Manjaro

If you install Manjaro with LUKS enabled, it automatically creates two keyslots and doesn't
tell you about them.

The first one is used for your passphrase you enter during installation, which is fine.

The second one is stored as keyfile under `/crypto_keyfile.bin`, which I just discovered
after years.

I don't know why it exists, but I don't want to have it.

Therefore, I

1. removed the file `sudo rm /crypto_keyfile.bin`
1. deleted the reference in `/etc/mkinitpcio.conf`
1. rebuild initramfs via `sudo mkinitpcio -P`
1. find the corresponding key slot
   I have used `sudo cryptsetup --verbose open --test-passphrase /dev/nvme0n1p2` to find the passphrase
   key slot, and deleted the other one.
1. deleted the key slot via `sudo cryptsetup --verbose luksKillSlot /dev/nvme0n1p2 N`
   (replace `N` by your key slot number)
