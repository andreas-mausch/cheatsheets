---
layout: cheatsheet
tags: cryptsetup security disk-encryption kdf key-derivation argon2 openssl aes
section:
  - name: Get disk serial number
    commands:
      inxi: sudo inxi -Dxxd
      udevadm: bash -c 'for dev in /dev/sd? /dev/nvme?n1; do udevadm info --query=all --name="$dev" | grep -E "DEVNAME|ID_SERIAL"; echo ---; done'
  - name: Prepare the disk
    commands:
      Complete wipe via dd (will destroy all data): sudo dd if=/dev/urandom of=/dev/sdX bs=8M iflag=fullblock status=progress
  - name: Generate key
    commands:
      via openssl and argon2: openssl kdf -binary -keylen 64 -kdfopt pass:(read --prompt-str 'Enter your password: ') -kdfopt salt:'HDD|Serial:123456789' -kdfopt iter:4 -kdfopt memcost:262144 -kdfopt lanes:4 Argon2id
  - name: Open disk
    commands:
      open: sudo cryptsetup open --type=plain --cipher=aes-xts-plain64 --key-file=./keyfile.bin --key-size=512 --keyfile-size=64 --offset=0 --hash=plain /dev/sdX my_container
      check status: sudo dmsetup ls --target crypt
      create filesystem: sudo mkfs.ext4 -m 0 /dev/mapper/my_container
---

Be careful with all the commands and double check everything you enter.

- Replace `/dev/sdX` with your real block device.
- Replace `123456789` with your real (short) disk serial number.
- Replace `my_container` with a name of your choice. Should be unique.

**You might experience permanent data loss if your command is wrong!**

Test the commands first with test drives to ensure they work as you expect.
Wiping the disk with dd will erase all your existing data.
Proceed with caution and always ensure that you have appropriate backups in place.
Use at your own risk.

# My parameters

- dm-crypt's Plain mode (= not LUKS)  
  I prefer it for not having a header on the disk,
  so it purely looks like random data.
- Key derivation function: **Argon2**
- Salt (S): **HDD|Serial:123456789**
- Memory cost (m, in KiB): 262144 (which is 256 MB)
- Iterations (t): 4
- Parallelism (p): 4 (it is called `lanes` in openssl)
- Key length: 64 bytes (= 512 bits)
- The default version (v) is used: 0x13 (= 19 decimal)

Note them. You need the exact same parameters each time you open the disk,
otherwise a different key is generated and the data is unreadable.

# Common usage

```bash
openssl kdf -binary -keylen 64 -kdfopt pass:(read --prompt-str 'Enter your password: ') -kdfopt salt:'HDD|Serial:123456789' -kdfopt iter:4 -kdfopt memcost:262144 -kdfopt lanes:4 Argon2id | sudo cryptsetup open --type=plain --cipher=aes-xts-plain64 --key-file=- --key-size=512 --keyfile-size=64 --offset=0 --hash=plain /dev/sdX my_container
udisksctl mount --filesystem-type=ext4 --block-device=/dev/mapper/my_container
# Use the disk here
udisksctl unmount --block-device=/dev/mapper/my_container
sudo cryptsetup close my_container
sudo udisksctl power-off --block-device=/dev/sdX
```

# Notes

## A note on the key length

We really only use a 256 bit key strength for the encryption,
but the cipher `aes-xts-plain64` in cryptsetup requires two keys.

## A note on hash

Important: Use `--hash=plain` when piping in the binary key from a command like openssl.
This cost me quite some time to figure out.
