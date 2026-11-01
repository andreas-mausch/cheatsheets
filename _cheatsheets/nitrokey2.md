---
layout: cheatsheet
tags: nitrokey nitrokey2 pro nitrocli nitropy security hardware token openpgp gpg otp secrets ssh udev
logo: data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGRhdGEtbmFtZT0iRWJlbmUgMSIgdmlld0JveD0iMCAwIDUwMCA1MDAiPjx0aXRsZT5aZWljaGVuZmzDpGNoZSAxMDwvdGl0bGU+PHBhdGggZD0iTTExOC4xIDI0Mi44M2ExNC4xOSAxNC4xOSAwIDAgMC01LjUyIDE5Ljg2bDU0LjA5IDk0LjkzYTE0LjE4IDE0LjE4IDAgMCAwIDE5Ljg2IDUuNTFsMTAxLjU1LTU5LjYtNjguNDMtMTE5LjJaTTI0NC4yNCAxODkuNDdsNTEuODggODkuNCA5Mi40LTU0LjgxLTUxLjg4LTg5LjR6Ii8+PHBhdGggZD0iTTQ0Mi42IDc3LjI2IDI2Ny4xMSAzLjMxYy0xMS00LjQxLTIzLjE4LTQuNDEtMzMuMTEgMEw1Ny40IDc4LjM3QzQwLjg0IDg1IDMwLjkxIDEwMS41NSAzMC45MSAxMTkuMjF2MTU2LjczYzAgNi42MiAyLjIgMTIuMTQgMy4zMSAxNi41NSAxMSAyMy4xOCA2Ni4yMiAxNTAuMTEgMTk5Ljc4IDIwNC4yIDYuNjIgMi4yMSAxMSAzLjMxIDE2LjU1IDMuMzEgNC40MiAwIDkuOTQtMi4yMSAxNS40NS01LjUyIDEzMy41Ni01NC4wOCAxODkuODUtMTc4LjgxIDE5OS43OC0yMDUuM2E0NC4yIDQ0LjIgMCAwIDAgMy4zMS0xNi41NVYxMTguMWMwLTE4Ljc2LTkuOTMtMzQuMjEtMjYuNDktNDAuODRtLTE1LjQ1IDE5Ni40N3YyLjIxYy04LjgzIDIyLjA3LTU3LjM5IDEzMy41NS0xNzcuNyAxODMuMjJoLTIuMjFDMTI5LjE0IDQxMC42IDc4LjM3IDI5OS4xMiA2OS41NCAyNzdWMTIwLjMxYzAtMi4yMSAyLjItMy4zMSAzLjMxLTQuNDJsMTc3LjctNzUgMTczLjI5IDc0YzIuMjEgMCAzLjMxIDIuMjEgMy4zMSA0LjQyWiIvPjwvc3ZnPg==
section:
  - name: Install
    commands:
      install nitropy (official): sudo pacman -S python-pynitrokey
      install nitrocli (third-party): sudo pacman -S nitrocli
      udev rules: sudo wget https://raw.githubusercontent.com/Nitrokey/libnitrokey/master/data/41-nitrokey.rules -O /etc/udev/rules.d/41-nitrokey.rules
      reload udev rules: sudo udevadm control --reload-rules && sudo udevadm trigger
  - name: Device
    commands:
      - title: list all attached devices
        command: nitrocli list
        options:
          -n: "--no-connect: skip serial numbers of Storage devices"
      - title: device status (serial, firmware, PIN retries)
        command: nitrocli status
      - title: lock the password safe
        command: nitrocli lock
      - title: select the device model
        command: nitrocli -m pro status
        options:
          -m: "librem, pro, or storage"
      - title: select by serial number (hex, optional 0x)
        command: nitrocli --serial-number 0x0123456789abcdef status
      - title: select by USB path
        command: nitrocli --usb-path 1-2 status
      - title: do not cache secrets in gpg-agent
        command: nitrocli --no-cache status
      - title: verbose logging (repeatable, up to 5 times)
        command: nitrocli -vvvvvv status
  - name: One-time passwords
    commands:
      - title: set a TOTP slot
        command: nitrocli otp set 0 github <secret> --algorithm totp
        options:
          -a: "hotp or totp (default: totp)"
          -d: "6 or 8 digits (default: 6)"
          -f: "ascii, base32 (default), or hex"
          -c: initial HOTP counter (default 0)
          -t: TOTP time window in seconds (default 30)
      - title: read the secret from stdin
        command: nitrocli otp set 0 github - --algorithm totp
      - title: set an HOTP slot with a counter
        command: nitrocli otp set 0 foo <secret> --algorithm hotp --counter 0
      - title: generate a code
        command: nitrocli otp get 0 --algorithm totp
      - title: generate a code for a fixed time (Unix timestamp)
        command: nitrocli otp get 0 -a totp --time 1700000000
      - title: list used slots
        command: nitrocli otp status --all
      - title: clear a slot
        command: nitrocli otp clear 0 --algorithm totp
  - name: Password safe
    commands:
      - title: add to the first free slot
        command: nitrocli pws add email me@example.com <password>
      - title: add to a specific slot (fails if taken)
        command: nitrocli pws add --slot 0 email me@example.com <password>
      - title: read the password from stdin
        command: nitrocli pws add email me@example.com -
      - title: read a slot
        command: nitrocli pws get 0
        options:
          -n: print only the name
          -l: print only the login
          -p: print only the password
          -q: "--quiet: no labels, just the values"
      - title: read only the password
        command: nitrocli pws get 0 --password --quiet
      - title: update one field
        command: nitrocli pws update 0 --password <new-password>
        options:
          -n: new name
          -l: new login
          -p: new password, or - to read from stdin
      - title: list used slots
        command: nitrocli pws status --all
      - title: clear a slot
        command: nitrocli pws clear 0
  - name: Firmware
    commands:
      list devices in update mode: nitropy pro list
      switch into update mode: nitropy pro enable-update
      switch in with a custom update password: nitropy pro enable-update -p <password>
      flash a firmware image: nitropy pro update nitrokey-pro-firmware-<version>.bin
      change the update password: nitropy pro change-firmware-password
      manual flash with dfu-util: dfu-util -D update_binary.bin
      released versions: "https://github.com/Nitrokey/nitrokey-pro-firmware/releases"
      note: "The update password defaults to 12345678 and the file name must end in .bin. In update mode the Pro 2 shows up as 20a0:42b4, not as 20a0:4108. Use Nitrokey App 1.5-RC7 or higher to switch the boot mode if nitropy fails."
  - name: SSH
    commands:
      enable the SSH agent: "echo 'enable-ssh-support' >> ~/.gnupg/gpg-agent.conf"
      set SSH_AUTH_SOCK: export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
      do it on every shell: "printf 'export SSH_AUTH_SOCK=\"$(gpgconf --list-dirs agent-ssh-socket)\"\n' >> ~/.bashrc"
      add the public key to a server: ssh-copy-id -i <(gpg --export-ssh-key <key>) user@server
      add the public key to GitHub: gpg --export-ssh-key <key> | xclip -selection clipboard
      list loaded keys: ssh-add -l
      show the agent's public key: cat ~/.gnupg/S.gpg-agent.ssh.pub
      restart the agent: pkill gpg-agent
      kill a stuck agent: gpgconf --kill gpg-agent
  - name: Troubleshooting
    commands:
      no device found: lsusb | grep 20a0:4108
      no permission on /dev/hidrawX: sudo chmod 660 /dev/hidraw0 && sudo chown root:plugdev /dev/hidraw0
      add the user to plugdev: sudo usermod -aG plugdev $USER
      watch udev events: udevadm monitor --property --udev
      find the USB product ID for a udev rule: "udevadm info -a -n /dev/hidraw0 | grep -i product"
      stop pcscd from grabbing the card (breaks gpg): sudo systemctl stop pcscd
      kill a running pcscd: sudo pkill pcscd
      gpg cannot see the card: gpgconf --kill gpg-agent dirmngr scdaemon && gpg --card-status
      raw APDU debugging: gpg --debug-level expert --card-edit
      verbose device communication: nitrocli -vvvvvv status
---

# Nitrokey Pro 2

Commands for the **Nitrokey Pro 2** (USB ID `20a0:4108`). For the Nitrokey 3
series see [nitrokey3]({{ '/nitrokey3/' | relative_url }}).

`nitropy` is the official Python tool from Nitrokey (`pynitrokey`). On the
Pro 2 it is only useful for firmware work via its `pro` subcommand.

`nitrocli` is a third-party Rust program that talks to the older HID-based
Nitrokeys: the Pro, the Storage and the Librem Key. It is the daily driver on
this sheet.

## Supported protocols and features

Per the compatibility matrices on the [Nitrokey feature
pages](https://docs.nitrokey.com/nitrokeys/features/index.html) and the
[Pro 2 FAQ](https://docs.nitrokey.com/nitrokeys/pro/faq.html):

| Protocol / feature           | Notes                                             |
|------------------------------|---------------------------------------------------|
| OpenPGP (GnuPG)              | OpenPGP Card 3.3                                  |
| SSH login                    | via OpenPGP / gpg-agent                           |
| TOTP                         | 15 slots                                          |
| HOTP                         | 3 slots                                           |
| Password safe                | 16 slots                                          |
| True random number generator | BSI TR-03116, ~40 kbit/s                          |
| S/MIME (X.509)               | signed / encrypted mail with an X.509 certificate |
| PKCS#11                      | token API (cryptoki)                              |

> The FAQ warns not to use GnuPG in parallel with OpenSC or another PKCS#11
> driver: `scdaemon` and OpenSC both want exclusive access to the card, so
> whichever got there first holds it. The documented symptom is that the
> tools hang each other - re-inserting the device clears it.

**Not supported.** There is no FIDO2 / WebAuthn and no PIV applet - both are
Nitrokey 3 features, and so is the KeePassXC challenge-response and the touch
confirmation (UIF), which the Pro 2 also can't do hardware-wise: it has no
touch sensor. Ed25519 and Curve25519 keys are out too. Also, no mass storage.

> U2F is documented inconsistently: the Pro 2 landing page links the U2F
> guides, but the U2F compatibility matrix lists the Pro 2 as *inactive*.
> Treat U2F as not available.

## Default PINs and passwords

| Purpose                  | Default    | Minimum | Tries |
|--------------------------|------------|---------|-------|
| OpenPGP user PIN         | `123456`   | 6       | 3     |
| OpenPGP admin PIN        | `12345678` | 8       | 3     |
| OpenPGP reset code       | none       | 8       | 3     |
| Firmware update password | `12345678` | —       | —     |

`nitrocli pin unblock` (or `gpg --card-edit → admin → passwd → (2)`) resets
a blocked user PIN with the admin PIN. If the **admin** PIN counter hits zero,
the only way out is a factory reset - so back up your admin PIN somewhere safe.

The firmware update password has no retry counter, but if you lose it the
device **cannot be firmware-updated anymore**. Change it with
`nitropy pro change-firmware-password`.

The user PIN serves OpenPGP operations, OTP generation and the password safe.
There is no separate OTP PIN - `otp get` requires the same user PIN unless
`--no-otp-pin` is set in the configuration. Once unlocked, the password safe
is readable without further authentication until `nitrocli lock` or a power
cycle.

## Slot limits

| Storage       | Count | Numbering |
|---------------|-------|-----------|
| HOTP slots    | 3     | 0-2       |
| TOTP slots    | 15    | 0-14      |
| Password safe | 16    | 0-15      |

Slots are numbered **per algorithm**, so TOTP slot 0 and HOTP slot 0 are
different slots. TOTP also needs the device clock to be in sync - `otp get`
syncs it from the system clock unless you pass `--time`.

## Harden security for production

All credentials ship with well-known defaults. Before using the device for
anything real, change them. PINs can be up to 32 characters (digits, letters,
special characters; the Nitrokey App does not support that many) - but with
only 3 tries the lockout is the real protection, not length.

```bash
nitrocli pin set admin            # min 8, factory default: 12345678
nitrocli pin set user             # min 6, factory default: 123456
nitropy pro change-firmware-password  # no lockout, but unrecoverable if lost
```

Optionally, set a reset code so a helper can unblock the user PIN without
knowing the admin PIN:

```bash
gpg --card-edit
gpg/card> admin
gpg/card> passwd
# choose (4) reset code, min 8 characters
```

> Once a reset code is set it **cannot be disabled** - only resetting the
> OpenPGP card clears it.

## Factory reset

> **Destructive and unrecoverable.** OpenPGP keys generated on the device never
> leave it, so if you have not run `gpg --export-secret-keys --armor` you have
> no way back. Do that first.

### Which reset do I need?

| Situation                                  | Use                                      |
|--------------------------------------------|------------------------------------------|
| Admin PIN counter hit 0, device is bricked | whole-device `nitrocli reset`            |
| OpenPGP keys lost or compromised           | OpenPGP-only reset via `gpg`             |
| Key is being sold or given away            | whole-device `nitrocli reset`            |
| Forgot the user PIN, admin PIN still works | `nitrocli pin unblock` - no reset needed |

The three resets differ in scope:

| Property               | OpenPGP reset  | Whole-device reset | New AES key    |
|------------------------|----------------|--------------------|----------------|
| Requires admin PIN     | no             | yes                | yes            |
| Destroys OpenPGP keys  | yes            | yes                | no             |
| Destroys password safe | clears the key | yes                | clears the key |
| Destroys OTPs          | no             | yes                | no             |

Worth knowing about the "clears the key" rows: Nitrokey notes that they leave
the encrypted data on the device but discard the key needed to read it, and
the `nitrocli` manpage goes further - it claims the AES key encrypts "the
password safe, the OTP slots and the encrypted volume". For the Pro 2, only
the password-safe part is true: the firmware reads OTP secrets straight from
flash with no decryption (see *OTP seeds are stored in plaintext* under
Physical attack surface). So `reset --only-aes-key` permanently clears the
PWS entries, but the OTP slots were never AES-protected in the first place.

### Step by step

**Whole device** - resets the OpenPGP card, wipes the flash storage and builds
a new AES key. The user PIN returns to `123456` and the admin PIN to
`12345678`:

```bash
nitrocli reset
```

`nitrocli` deliberately re-prompts for the admin PIN here even when gpg-agent
has it cached, so this cannot be triggered by accident.

**New AES key only** - same admin PIN, but keeps the OpenPGP keys and the OTP
slot definitions:

```bash
nitrocli reset --only-aes-key
```

**OpenPGP card only** - keeps the password safe and the OTP slots, useful when
only the OpenPGP keys are compromised:

```bash
gpg --card-edit
```

then `admin` (this prompts for the admin PIN) and finally `factory-reset`.

**Via Nitrokey App** - `Configure -> Special Configure -> Factory reset`. This
is an administrative function, so the App has to be started with `--admin` for
the menu entry to appear. The App always generates a new AES key.

## TOTP workflows

OTP slots live on the STM32 MCU, not on the OpenPGP card: GnuPG never sees
them, an OpenPGP-only factory reset does not touch them, and they are numbered
per algorithm (see the slot limits section above).

### Add an account

Enroll at the website, follow the "can't scan the QR code?" link, and write the
Base32 secret to a free slot:

```bash
nitrocli otp set 0 github JBSWY3DPEHPK3PXP -a totp
```

Only have the QR image? Extract the secret first - the device does not parse
`otpauth://` URIs:

```bash
zbarimg --raw github-otp.png
# otpauth://totp/GitHub:me?secret=JBSWY3DPEHPK3PXP&issuer=GitHub
```

Keep the site's recovery codes somewhere off-device, or a broken or reset
stick locks you out for good.

### Get the current token

```bash
nitrocli otp get 0            # prompts for the user PIN; HOTP: -a hotp
```

`otp get` syncs the device clock from your system clock first, so a stick that
sat in a drawer for months still produces correct codes. `--time <unix>`
computes for a fixed timestamp. `config set -O` drops the PIN requirement -
convenience on your own machine, no protection anywhere else. If the stick is
ever lost, treat its accounts as compromised - see
*OTP seeds are stored in plaintext* under Physical attack surface.

### Rotate, list, remove

```bash
nitrocli otp status --all              # used slots and their names
nitrocli otp set 0 github <secret> -a totp   # overwrite an occupied slot
nitrocli otp clear 0 -a totp           # wipe a slot
```

Slot numbers are per algorithm: `clear 0 -a totp` leaves HOTP slot 0 alone.

## OpenPGP / GPG workflows

### Move an existing key to the card

Inspect the key first - the subkeys and their capabilities (`sc` / `e` / `a`),
fingerprints and keygrips. The keygrips are what `scdaemon` later maps to the
card slots, and `show-unusable-subkeys` also lists expired or revoked ones:

```bash
gpg --list-secret-keys --keyid-format long --with-keygrip \
    --with-subkey-fingerprints \
    --list-options=show-unusable-subkeys,show-pref-verbose
```

> `keytocard` **deletes** the key from the local keyring (only a stub remains).
> Export a backup first if you need one.

```bash
gpg --export-secret-keys --armor <key> > backup.asc   # back up first
gpg --edit-key --expert <key>
```

Inside `gpg>`:

| Step                              | Command           | Slot           |
|-----------------------------------|-------------------|----------------|
| Select primary key (none starred) | `keytocard` → `1` | Signature      |
| `key 1` (star the first subkey)   | `keytocard` → `2` | Encryption     |
| `key 1` then `key 2`              | `keytocard` → `3` | Authentication |
| Finish                            | `quit` → `y`      |                |

Then set the card metadata:

```bash
gpg --card-edit
gpg/card> admin
gpg/card> name
gpg/card> url
```

The card has exactly three key slots: 1 = sign, 2 = encrypt, 3 = auth.
Supported algorithms on the Pro 2:

- RSA 2048 / 3072 / 4096
- NIST-P 256 / 384 / 521
- Brainpool 256r1 / 384r1 / 512r1

Not supported: Ed25519, Curve25519, secp256k1 (Nitrokey 3 only for the first
two). See
<https://docs.nitrokey.com/de/nitrokeys/pro/faq#which-algorithms-and-maximum-key-length-are-supported>
for the full table.

### Generate a new key on the card

```bash
gpg --card-edit
gpg/card> admin
gpg/card> name            # cardholder name, appears in pinentry prompts
gpg/card> url             # URL where the public key is hosted (e.g. keys.example.com/<fpr>.asc)
gpg/card> generate
```

Prompts for name, email and a passphrase. Generates all three keys (sign,
encrypt, auth) directly on the smart card - they **never leave the device**.
No backup is possible for on-card-generated keys unless you use `keytocard`
with an off-card-generated key instead.

Default is RSA-2048. To use ECC instead (requires OpenPGP Card version 3.3,
which the Pro 2 has):

```bash
gpg-connect-agent "SCD SETATTR KEY-ATTR --force 1 19 brainpoolP256r1" /bye
gpg-connect-agent "SCD SETATTR KEY-ATTR --force 2 18 brainpoolP256r1" /bye
gpg-connect-agent "SCD SETATTR KEY-ATTR --force 3 19 brainpoolP256r1" /bye
gpg --card-edit
gpg/card> generate
```

### Use the card on another machine

```bash
gpg --import pubkey.asc        # public key only
gpg --card-status              # links local keyring to card keys
```

Or if you set a URL on the card: `gpg --card-edit` → `fetch`.

### Export the public key

```bash
gpg --armor --export <key> > pubkey.asc
```

## nitrocli extensions

Any executable named `nitrocli-*` found on `$PATH` becomes a subcommand. For
example a `nitrocli-otp-cache` executable is invoked as `nitrocli otp-cache`.
See <https://github.com/d-e-s-o/nitrocli>.

## Physical attack surface

The Nitrokey Pro 2 has two chips with separate attack surfaces:

| Component  | Chip                           | Stores                             | Updateable via                 |
|------------|--------------------------------|------------------------------------|--------------------------------|
| MCU        | ST STM32F103TB (72 MHz)        | OTP secrets, password safe entries | DFU (software), SWD (hardware) |
| Smart card | NXP SmartMX P5CD081 (CC EAL5+) | OpenPGP keys, AES key, PINs        | not via DFU or SWD             |

### Unsigned firmware updates

The firmware on the STM32 is **not signed** - anyone who can run
`nitropy pro enable-update` and flash via DFU can install arbitrary firmware.
The update password is the only gate. What implant firmware would collect:
the OTP seeds (see *OTP seeds are stored in plaintext* below). OpenPGP keys
are unaffected by a reflash: they never leave the NXP chip.

| Attack                                                      |          Password protects?           |
|-------------------------------------------------------------|:-------------------------------------:|
| `nitropy pro enable-update` via USB (~10 s physical access) |                  yes                  |
| SWD programmer (open case, solder pads)                     |                  no                   |
| Extract keys from the NXP chip                              | no (but EAL5+ makes this impractical) |

The password guards against opportunistic USB attacks, not against targeted
hardware attacks. If you lose it, the device cannot be firmware-updated
anymore - there is no recovery.

### OTP seeds are stored in plaintext

Not encrypted, not PIN-bound - raw secrets in MCU flash. Verified in the
firmware source: the code generators (`src/hotp/hotp.c`,
`get_code_from_totp_slot` / `get_code_from_hotp_slot`) feed the flash bytes
straight into the HMAC; the file contains no decryption step because there is
nothing to decrypt. What a thief gets from your stick:

| On the stick         | Survives theft? | Why                                              |
|----------------------|-----------------|--------------------------------------------------|
| OpenPGP keys         | yes             | separate EAL5+ smart card, PIN-gated             |
| Password safe        | yes             | AES-encrypted; key (PIN-protected) on smart card |
| **All 18 OTP seeds** | **no**          | plaintext flash, two extraction paths            |

**Path 1, the cheap one (software).** Via the unsigned updates above. With
~10 s of USB access and the firmware update password (default `12345678`,
unchanged unless you changed it), an attacker flashes custom firmware via DFU,
and the stick reports its own OTP slots back - the device can even *type* them
into a text editor.

**Path 2 (hardware).** The STM32F103's read-out protection is bypassed by
public, cheap attacks (F1XOR, STM32F1 Break); an opened case with SWD pads is
easier still. No PIN helps: the PIN gates the command interface, never the
storage.

Consequences:

- `nitropy pro change-firmware-password` is the *only* software defense for
  path 1, and it is not optional.
- `nitrocli lock` changes nothing here - it zeroes the password-safe key in
  RAM and never touches the OTP flash.
- Treat a lost stick as **all TOTP accounts compromised**: keep recovery
  codes for every enrolled account somewhere separate.
- Nothing configured on a Pro 2 fixes this - the MCU has no secure element
  for the OTP store. High-value accounts belong on hardware with signed
  firmware and an encrypted OTP store ([nitrokey3]({{ '/nitrokey3/' | relative_url }})),
  or better on FIDO2, where there is no seed to steal at all.

## Sources

- <https://man7.org/linux/man-pages/man1/nitrocli.1.html>
- <https://docs.nitrokey.com/nitrokeys/pro/cli>
- <https://docs.nitrokey.com/nitrokeys/pro/faq>
- <https://docs.nitrokey.com/nitrokeys/features/index>
- <https://docs.nitrokey.com/nitrokeys/pro/firmware-update>
- <https://github.com/Nitrokey/pynitrokey>
- <https://github.com/Nitrokey/nitrokey-pro-firmware> - OTP storage and code generation in `src/hotp/hotp.c`
- <https://blog.zapb.de/stm32f1-exceptional-failure/> - fault-injection break of the STM32F1 read-out protection
- <https://support.nitrokey.com/t/breaking-the-stm32f1-read-out-protection/2186> - Nitrokey's own reaction to that attack
- <https://www.gnupg.org/documentation/manuals/gnupg26/gpg-card.html>
