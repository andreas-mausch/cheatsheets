---
layout: cheatsheet
tags: nitrokey nitrokey3 nfc nitropy security hardware token fido2 openpgp gpg totp otp piv secrets ssh pam pcsc udev
logo: data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGRhdGEtbmFtZT0iRWJlbmUgMSIgdmlld0JveD0iMCAwIDUwMCA1MDAiPjx0aXRsZT5aZWljaGVuZmzDpGNoZSAxMDwvdGl0bGU+PHBhdGggZD0iTTExOC4xIDI0Mi44M2ExNC4xOSAxNC4xOSAwIDAgMC01LjUyIDE5Ljg2bDU0LjA5IDk0LjkzYTE0LjE4IDE0LjE4IDAgMCAwIDE5Ljg2IDUuNTFsMTAxLjU1LTU5LjYtNjguNDMtMTE5LjJaTTI0NC4yNCAxODkuNDdsNTEuODggODkuNCA5Mi40LTU0LjgxLTUxLjg4LTg5LjR6Ii8+PHBhdGggZD0iTTQ0Mi42IDc3LjI2IDI2Ny4xMSAzLjMxYy0xMS00LjQxLTIzLjE4LTQuNDEtMzMuMTEgMEw1Ny40IDc4LjM3QzQwLjg0IDg1IDMwLjkxIDEwMS41NSAzMC45MSAxMTkuMjF2MTU2LjczYzAgNi42MiAyLjIgMTIuMTQgMy4zMSAxNi41NSAxMSAyMy4xOCA2Ni4yMiAxNTAuMTEgMTk5Ljc4IDIwNC4yIDYuNjIgMi4yMSAxMSAzLjMxIDE2LjU1IDMuMzEgNC40MiAwIDkuOTQtMi4yMSAxNS40NS01LjUyIDEzMy41Ni01NC4wOCAxODkuODUtMTc4LjgxIDE5OS43OC0yMDUuM2E0NC4yIDQ0LjIgMCAwIDAgMy4zMS0xNi41NVYxMTguMWMwLTE4Ljc2LTkuOTMtMzQuMjEtMjYuNDktNDAuODRtLTE1LjQ1IDE5Ni40N3YyLjIxYy04LjgzIDIyLjA3LTU3LjM5IDEzMy41NS0xNzcuNyAxODMuMjJoLTIuMjFDMTI5LjE0IDQxMC42IDc4LjM3IDI5OS4xMiA2OS41NCAyNzdWMTIwLjMxYzAtMi4yMSAyLjItMy4zMSAzLjMxLTQuNDJsMTc3LjctNzUgMTczLjI5IDc0YzIuMjEgMCAzLjMxIDIuMjEgMy4zMSA0LjQyWiIvPjwvc3ZnPg==
section:
  - name: Install
    commands:
      install nitropy: sudo pacman -S python-pynitrokey
      install with PIV support: 'pipx install "pynitrokey[pcsc]"'
      udev rules: sudo wget https://raw.githubusercontent.com/Nitrokey/libnitrokey/master/data/41-nitrokey.rules -O /etc/udev/rules.d/41-nitrokey.rules
      reload udev rules: sudo udevadm control --reload-rules && sudo udevadm trigger
  - name: Device
    commands:
      - title: list all connected Nitrokeys
        command: nitropy list
      - title: list Nitrokey 3 devices
        command: nitropy nk3 list
      - title: firmware version
        command: nitropy nk3 version
      - title: device and app status
        command: nitropy nk3 status
      - title: blink the LED to find the device
        command: nitropy nk3 wink
      - title: reboot into bootloader mode
        command: nitropy nk3 reboot --bootloader
      - title: select a device by path
        command: nitropy nk3 --path /dev/hidraw3 version
  - name: Random number generator
    commands:
      - title: random data from the TRNG
        command: nitropy nk3 rng --length 32
  - name: Configuration
    commands:
      - title: list all config fields
        command: nitropy nk3 list-config-fields
      - title: read a value
        command: nitropy nk3 get-config <key>
      - title: set a value
        command: nitropy nk3 set-config <key> <value>
      - title: set a value, check only
        command: nitropy nk3 set-config --dry-run <key> <value>
      - title: set a field nitropy does not know
        command: nitropy nk3 set-config --force <key> <value>
        source: https://github.com/Nitrokey/pynitrokey/blob/main/pynitrokey/cli/trussed/__init__.py
      - title: is the OpenPGP app using the secure element?
        command: nitropy nk3 get-config opcard.use_se050_backend
      - title: note
        command: "Changing config can have side effects. The device reboots automatically if needed."
  - name: Troubleshooting
    commands:
      no device found: lsusb | grep 20a0:42b2
      no permission on /dev/hidrawX (temporary, lost on replug): sudo setfacl -m u:$USER:rw /dev/hidraw0
      persistent group fix (plugdev is Debian/Ubuntu only): sudo usermod -aG plugdev $USER
      watch udev events: udevadm monitor --property --udev
      find the USB product ID for a udev rule: "udevadm info -a -n /dev/hidraw0 | grep -i product"
      is the card visible to PC/SC (shows OpenPGP and PIV applets): pcsc_scan
      list readers the OpenSC way: opensc-tool --list-readers
      list PKCS#11 modules: p11-kit list-modules
      dump PKCS#11 objects: p11tool --list-all
      pcscd and gpg conflict over the card - hand it to gpg: sudo systemctl stop pcscd
      kill a running pcscd: sudo pkill pcscd
      gpg cannot see the card: gpgconf --kill gpg-agent dirmngr scdaemon && gpg --card-status
      raw APDU debugging: gpg --debug-level expert --card-edit
      nitropy debug log: cat /tmp/nitropy.log.*
      run against a specific device: nitropy nk3 --path /dev/hidraw0 status
      macOS keeps grabbing the device: nitropy nk3 reboot --bootloader
---

# Nitrokey 3C NFC

Commands for the **Nitrokey 3** family, including the Nitrokey 3C NFC (USB ID
`20a0:42b2`). For the older HID-based devices see
[nitrokey2]({{ '/nitrokey2/' | relative_url }}).

The Nitrokey 3 runs several independent apps on the same hardware: OpenPGP
card, FIDO2, a secrets app (TOTP and passwords) and an experimental PIV app.
Each has its **own PIN with its own retry counter**, and each can be factory
reset on its own.

## Which tool for which app

| Feature                  | Protocol / Standard           | What it does                                | Tool                             | Notes                                                         |
|--------------------------|-------------------------------|---------------------------------------------|----------------------------------|---------------------------------------------------------------|
| Device, firmware, config | Nitrokey management (USB HID) | status, signed updates, diagnostics, config | `nitropy nk3`                    |                                                               |
| Passkeys, 2FA            | FIDO2 / WebAuthn (CTAP2)      | possession-based login, no secret to leak   | browser, `nitropy fido2`         | ~30 resident keys (3A Mini: 100), unlimited non-resident, NFC |
| Legacy 2FA               | U2F (CTAP1)                   | backward compatible                         | browser                          |                                                               |
| Mail & file encryption   | OpenPGP Card 3.4.1            | three keys: sign / encrypt / auth           | `gpg`, `gpg-card`                | touch confirmation (UIF), SE050 secure element default        |
| SSH login                | SSH via `gpg-agent`           | card's auth key serves OpenSSH              | `gpg-agent`                      | `enable-ssh-support`                                          |
| One-time passwords       | TOTP / HOTP (RFC 6238/4226)   | time- or counter-based codes                | `nitropy nk3 secrets`            | 6/8 digits, SHA1/256, per-entry touch or PIN                  |
| Passwords                | secrets app (proprietary)     | static logins and passwords                 | `nitropy nk3 secrets`            | up to 50 entries                                              |
| Challenge-response       | HMAC-SHA1 (Yubico-compatible) | KeePassXC keyfile protection                | `nitropy nk3 secrets`            | 2 slots; FIDO2 credentials can also carry HMAC-secret         |
| Windows / TLS login      | PIV (NIST SP 800-73)          | key slots with X.509 certificates           | `nitropy nk3 piv --experimental` | experimental, up to 24 key pairs                              |
| Generic token API        | PKCS#11 (cryptoki)            | exposes keys to non-GnuPG apps              | `p11-kit`, `p11tool`, OpenSC     | browsers, PAM, OpenSSL - conflicts with scdaemon              |
| Raw APDUs                | ISO 7816                      | direct applet access through pcscd          | `opensc-tool`, `pcsc_scan`       | escape hatch, e.g. PIV factory reset                          |
| Random                   | TRNG                          | random bytes                                | `nitropy nk3 rng`                |                                                               |

The Nitrokey App 2 GUI can also do all of the above, including TOTP and
password storage.

> As on the Pro 2: don't use GnuPG and an OpenSC PKCS#11 driver against the
> card at the same time - `scdaemon` and OpenSC both want exclusive access,
> and the one that got there first wins. The tools hang; re-inserting clears
> it.

Since firmware 1.7.0 the OpenPGP app uses the **SE050M secure element**
(Common Criteria EAL6+ by default, PIV follows since 1.8.0); check the config
field `opcard.use_se050_backend`. Supported algorithms
([FAQ](https://docs.nitrokey.com/nitrokeys/nitrokey3/faq)):

| Key type              | OpenPGP (with SE) | OpenPGP (without SE) | PIV |
|-----------------------|-------------------|----------------------|-----|
| Ed25519 / Curve25519  | yes               | yes                  |     |
| NIST P-256            | yes               | yes                  | yes |
| NIST P-384 / P-521    | yes               |                      |     |
| Brainpool 256/384/512 | yes               |                      |     |
| RSA-2048              | yes               | yes                  | yes |
| RSA-3072 / RSA-4096   | yes               | import only          |     |
| secp256k1             | yes               |                      |     |

**Not supported.** No encrypted mass storage (the key stores only crypto
material). The PIV app is experimental; the docs table above only certifies
RSA-2048 and NIST P-256 there, even though `nitropy` also offers
rsa3072/rsa4096 and nistp384.

## Default PINs and PIN rules

| Purpose                  | Default                          | Rules               | Tries |
|--------------------------|----------------------------------|---------------------|-------|
| OpenPGP user PIN         | `123456`                         | 6-127 characters    | 3     |
| OpenPGP admin PIN        | `12345678`                       | 8-127 characters    | 3     |
| OpenPGP reset code       | none                             | 8-127 characters    | 3     |
| FIDO2 PIN                | none                             | 4+ characters       | 8 *   |
| Secrets app PIN          | none                             | 6+ characters       | 8     |
| PIV PIN                  | `123456`                         | 6-8 decimal digits  | 3     |
| PIV PUK                  | `12345678`                       | 8 characters        | 3     |
| PIV management key (MGM) | `0102030405060708...` (24 bytes) | hex key, no lockout | -     |

\* FIDO2 deliberately does **not** lock permanently: after every 3 failed
attempts Nitrokey resets the counter when you unplug the device. 8 failed
attempts still disable the PIN until `nitropy fido2 reset`.

If the OpenPGP **admin** PIN counter hits zero, the app is unusable until it
is factory reset - so change the defaults right away (in each app's workflow).
The reset code lets somebody unblock the user PIN without full admin rights,
but it can never be removed once set.

> **The PUK myth:** Nitrokey's reset page contains the APDU data
> `3333333333333333`, which is easy to misread as a secret default PUK. It is
> not - see the raw APDU breakdown in the factory reset workflow. The PIV PUK
> default is `12345678`, like every other Nitrokey secret.

## `gpg/card>` commands

Inside `gpg --card-edit`:

| Command                      | Purpose                                                              |
|------------------------------|----------------------------------------------------------------------|
| `help` / `list`              | list all available commands                                          |
| `show`                       | show the card's data                                                 |
| `generate`                   | generate a key on the card and write it                              |
| `keytocard [n]`              | move a subkey to the card                                            |
| `passwd`                     | change/unblock PINs (menu: 1 user, 2 unblock, 3 admin, 4 reset code) |
| `admin`                      | enter admin mode                                                     |
| `unblock`                    | unblock the user PIN with the reset code                             |
| `uif <n> on\|off\|permanent` | touch confirmation (needs `--expert`)                                |
| `verify`                     | verify a PIN                                                         |
| `erase`                      | delete a key from the card                                           |
| `factory-reset`              | wipe the OpenPGP app                                                 |
| `fetch`                      | fetch a key from the card's URL                                      |
| `name` / `url`               | card holder name and key URL                                         |
| `lang` / `sex` / `dob`       | personal data fields                                                 |
| `setattr <n> <op> <value>`   | set key attributes directly                                          |
| `bye`                        | leave the card editor                                                |

## PIV key slots

| Slot      | Usage                                                  |
|-----------|--------------------------------------------------------|
| `9A`      | Authentication (Windows smart-card login maps to this) |
| `9C`      | Signature                                              |
| `9D`      | Key management (encryption)                            |
| `9E`      | Card authentication (physical access control)          |
| `82`-`95` | Retired key management                                 |

Up to 24 key pairs in total; `--key` takes the slot as two hex digits.

## Firmware update

Exactly one Nitrokey 3 may be connected, in firmware or bootloader mode:

```bash
nitropy nk3 update                      # fetch and install the latest release
nitropy nk3 update --version <version>  # a specific release instead
nitropy nk3 update <firmware.bin>       # a local image
nitropy nk3 update --confirm            # skip the confirmation prompt
```

Offline or air-gapped: download the image first (`fetch-update [path]`, with
`--force` to overwrite and `--version` to pick a release), then check it
before flashing it with the local-image form above:

```bash
nitropy nk3 validate-update <firmware.bin>
```

## Factory reset

> **Destructive and unrecoverable.** OpenPGP keys generated on the device never
> leave it, so export a backup first. Because the Nitrokey 3 runs independent
> apps, you can almost always reset just the one that is broken instead of the
> whole device - prefer that.

### Which reset do I need?

| Situation                            | Use                                            |
|--------------------------------------|------------------------------------------------|
| Selling or giving the device away    | `nitropy nk3 factory-reset` (everything)       |
| OpenPGP admin PIN counter hit 0      | `nitropy nk3 factory-reset-app opcard`         |
| FIDO2 PIN counter hit 0              | `nitropy fido2 reset`                          |
| Secrets PIN counter hit 0            | `nitropy nk3 secrets reset --force`            |
| PIV PIN counter hit 0                | `nitropy nk3 piv --experimental factory-reset` |
| One app misbehaves, the rest is fine | the per-app reset for that app                 |

`factory-reset-app` only accepts `opcard` - use the per-app commands above for
everything else.

### Step by step

**Everything** - wipes all apps at once:

```bash
nitropy nk3 factory-reset
```

**OpenPGP app only** - leaves FIDO2, secrets and PIV untouched:

```bash
nitropy nk3 factory-reset-app opcard
```

or without nitropy:

```bash
gpg --card-edit
```

then `admin` and `factory-reset`.

Both of these ask you to **touch the device** to confirm.

**FIDO2 app only** - the reset window is the awkward part. The command is only
accepted within **10 seconds of plugging the device in**, and then you have to
press the button twice. So: unplug the key, start the command, plug it in,
press the button.

```bash
nitropy fido2 reset --yes
```

On Windows this needs Administrator rights.

**Secrets app only** - wipes all TOTP and password credentials:

```bash
nitropy nk3 secrets reset --force
```

**PIV app only** - this will *not* work while the PIN counter is healthy. It
deliberately fails with `You first need to lock the PIN with 3 failed
attempts`, so enter a wrong PIN three times on purpose first, then:

```bash
nitropy nk3 piv --experimental factory-reset
```

Nitrokey documents the same reset as a raw APDU sequence that does the
blocking steps for you:

```bash
opensc-tool -s 00:A4:04:00:0B:A000000308000010000100 -s 00:20:00:80:08:3333333333333333 -s 00:20:00:80:08:3333333333333333 -s 00:20:00:80:08:3333333333333333 -s 00:FB:00:00
```

Decoded: the first APDU selects the PIV applet, the three `00:20:00:80`
(VERIFY with key reference `0x80` = the **PIN**, the PUK would be `0x81`)
verify the PIN with the wrong value `33333333` - i.e. block it deliberately -
and `00:FB:00:00` is Nitrokey's vendor factory-reset command, accepted only
while the PIN is blocked. So `3333333333333333` is **not** a hidden PUK
(write-ups also use `FFFFFFFFFFFFFFFF`, any wrong value works), and the route
works regardless of what your PIN or PUK are set to.

## TOTP and HOTP (secrets app)

Credentials live in the secrets app: its own PIN (unrelated to OpenPGP/FIDO2)
and retry counter (check with `secrets status`), and a store of up to 50
entries. If the counter hits zero, only a reset of the app helps - see the
factory reset workflow.

### Enroll an account

Set the secrets PIN once before first use. Then enroll at the website, follow
the "can't scan the QR code?" link, and write the Base32 secret to the device:

```bash
nitropy nk3 secrets status
nitropy nk3 secrets set-pin   # min 6 characters
nitropy nk3 secrets add-otp github JBSWY3DPEHPK3PXP --kind TOTP
nitropy nk3 secrets add-otp github "$(cat)" --kind TOTP   # no '-' stdin - source it via substitution
```

Only have the QR image? Extract the secret first - nitropy does not parse
`otpauth://` URIs:

```bash
zbarimg --raw github-otp.png
# otpauth://totp/GitHub:me?secret=JBSWY3DPEHPK3PXP&issuer=GitHub
```

Options for `add-otp`:

| Option               | Meaning                                                         |
|----------------------|-----------------------------------------------------------------|
| `--kind`             | `TOTP`, `HOTP`, `HOTP_REVERSE` (reversed digits, Steam), `HMAC` |
| `--digits-str`       | 6 or 8 digits                                                   |
| `--hash`             | `SHA1` or `SHA256`                                              |
| `--counter-start`    | initial HOTP counter                                            |
| `--touch-button`     | require a button press to read                                  |
| `--protect-with-pin` | require the secrets PIN to read                                 |

Example, hardened variant: `nitropy nk3 secrets add-otp gitlab <secret> --kind
TOTP --digits-str 8 --hash SHA256 --touch-button --protect-with-pin`.

### Get the current code

```bash
nitropy nk3 secrets get-otp github
nitropy nk3 secrets get-otp github --period 30 --timestamp <unix>
nitropy nk3 secrets verify github <code>    # check a typed code against the stored one
```

Keep the site's recovery codes somewhere off-device anyway - a reset or broken
stick means re-enrolling every account from scratch. For renaming and
single-field updates, see the Passwords workflow below.

## Passwords (secrets app)

Same store and PIN as TOTP, up to 50 entries:

```bash
nitropy nk3 secrets status
nitropy nk3 secrets add-password email --login me@example.com --password <password>
nitropy nk3 secrets get-password email --password
```

`add-password` supports `--login`, `--metadata`, `--touch-button` and
`--protect-with-pin` like `add-otp`.

### Rename and update

Works for every credential in the store, passwords and OTPs alike:

```bash
nitropy nk3 secrets rename github github-work
nitropy nk3 secrets update email --password <new-password>
nitropy nk3 secrets update github --touch-button false # or --metadata <string>
```

### KeePassXC (challenge-response)

```bash
nitropy nk3 secrets add-challenge-response 1 <secret>   # slot 1 or 2; secret decodes to exactly 20 bytes
```

The Nitrokey App 2 has a KeePassXC wizard that does this graphically.
KeePassXC also accepts a FIDO2 credential with an HMAC-secret instead.

## OpenPGP / GnuPG keys

The card must be firmware > 1.4.0 for GnuPG to see it. Entry point for
everything interactive: `gpg --card-edit` (add `--expert` for `uif` and
`setattr`, `--reader <n>` when several readers are attached), commands listed
in the `gpg/card>` table above.

### Change and unblock PINs

In `gpg/card>`: `passwd` -> (1) user PIN, `admin` + `passwd` -> (3) admin PIN -
change both factory defaults (`123456` / `12345678`) before real use. (4) sets
an optional reset code, which unblocks the user PIN via `gpg/card>` -> `unblock`
without exposing the admin PIN. `admin` + `passwd` -> (2) also unblocks the
user PIN, and with the admin counter at zero there is no unlock left - factory
reset the OpenPGP app. From the shell (gpg-card): `gpg-card passwd 1` (user) /
`gpg-card passwd 3` (admin) - the PINs themselves are still entered via
pinentry, and the reset code has no own command (it is option 4 of the `passwd`
menu).

### Move an existing key to the card

Inspect the key first - subkeys, capabilities, keygrips. The keygrips are what
`scdaemon` maps to the card slots, and `show-unusable-subkeys` also lists
expired or revoked ones:

```bash
gpg --list-secret-keys --keyid-format long --with-keygrip \
    --with-subkey-fingerprints \
    --list-options=show-unusable-subkeys,show-pref-verbose
```

> `keytocard` **deletes** the key from the local keyring (only a stub remains).
> Back up first if you need one.

```bash
gpg --export-secret-keys --armor <key> > backup.asc   # back up first
gpg --edit-key --expert <key>
```

Inside `gpg>`:

| Step                              | Command            | Slot           |
|-----------------------------------|--------------------|----------------|
| Select primary key (none starred) | `keytocard` -> `1` | Signature      |
| `key 1` (star the first subkey)   | `keytocard` -> `2` | Encryption     |
| `key 1` then `key 2`              | `keytocard` -> `3` | Authentication |
| Finish                            | `quit` -> `y`      |                |

Then set the card metadata: `gpg/card>` -> `admin`, `name`, `url`.

### Generate a new key on the card

`gpg --card-edit` -> `admin`, `name`, `url`, then `generate`. Prompts for name,
email and a passphrase; generates all three keys (sign, encrypt, auth) on the
card - they **never leave the device**, so the backup.asc trick above is not
available afterwards.

Default is RSA-2048. For Ed25519/Curve25519 instead (slot 1 = sign, 2 =
encrypt):

```bash
gpg-connect-agent "SCD SETATTR KEY-ATTR --force 1 19 eddsa" /bye
gpg-connect-agent "SCD SETATTR KEY-ATTR --force 2 18 cv25519" /bye
```

then `generate` again. Other curves per the algorithm table above.

### Touch confirmation (UIF)

The Nitrokey 3 has a touch sensor, so every key operation can additionally
require a button press. In `gpg --card-edit --expert`: `uif 1 on` (sign),
`uif 2 on` (decrypt), `uif 3 on` (auth); `off` disables, `permanent` locks the
requirement in so it **can never be turned off**. From the shell (gpg-card):
`gpg-card uif 1 on`. The current setting shows in the card status output.

### Use the card on another machine

```bash
gpg --import pubkey.asc        # public key only
gpg --card-status              # links local keyring to card keys
```

Or if you set a URL on the card: `gpg/card>` -> `fetch`.

### Export the public key

```bash
gpg --armor --export <key> > pubkey.asc
```

Deleting a key from the card: `gpg/card>` -> `admin`, `erase`. To restore a
backup onto a fresh card: import `backup.asc`, then `keytocard` as above.

### LUKS disk unlock

Store a LUKS keyfile encrypted to the card's GPG key - the passphrase prompt
is replaced by the card PIN:

```bash
gpg --decrypt cryptkey.gpg | sudo cryptsetup open --key-file - <device> <name>
sudo cryptsetup luksChangeKey <device>      # change the LUKS passphrase
sudo cryptsetup luksRemoveKey <device>      # remove a key slot
```

The card can also unlock LUKS automatically via PAM (`pam_pkcs11` + OpenSC);
the Nitrokey App 2 can export the keys and certs needed for it.

## SSH login

Have `gpg-agent` serve the card's authentication subkey (slot 3) to OpenSSH.
Enable it once, then distribute the public key:

```bash
echo 'enable-ssh-support' >> ~/.gnupg/gpg-agent.conf
gpgconf --kill gpg-agent                    # restart to pick the setting up
export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
printf 'export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"\n' >> ~/.bashrc
```

```bash
gpg --export-ssh-key <key> | ssh user@server 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'   # ssh-copy-id -i rejects <(...) pipes
gpg --export-ssh-key <key> | xclip -selection clipboard   # paste into GitHub etc.
ssh-add -l
```

No GnuPG on the server side needed - it just sees an ordinary SSH public key.
FIDO2 alternative without the OpenPGP app: `ssh-keygen -t ed25519-sk` (OpenSSH
>= 8.1); add `-O verify-required` to make every login confirm by touch.

## FIDO2 and passkeys

```bash
nitropy fido2 get-info            # AAGUID, firmware, supported extensions
nitropy fido2 wink                # blink the LED to find the key
nitropy fido2 set-pin             # ships without a PIN - set one before enrolling
nitropy fido2 change-pin          # rotations later
```

Enroll passkeys in the browser as with any security key - no nitropy needed.
Unblocking after wrong attempts: 3 failures only block until you unplug and
replug; after 8 the PIN stays dead until you reset the app - factory reset
workflow. Manage what is on the key:

```bash
nitropy fido2 list-credentials          # asks for the PIN
nitropy fido2 delete-credential --cred-id <id>
```

Resident (discoverable) credentials take device memory - roughly 30 on the
Nitrokey 3 NFC, 100 on the 3A Mini; non-resident credentials (many corporate
SSOs) are unlimited.

### Test the key

```bash
nitropy fido2 verify              # built-in self test
nitropy fido2 make-credential --host example.com --user me                       # throwaway credential
nitropy fido2 challenge-response <cred-id> <challenge> --host example.com       # HMAC-secret proof of possession
```

`challenge-response` exercises the HMAC-secret extension - the same mechanism
KeePassXC (see the Passwords workflow) or clevis use to bind a secret to the
key plus presence.

### Login on Linux (pam_u2f)

Simplest full-disk-login option - flag names vary by version, check
`pamu2fcfg --help`:

```bash
# registers a credential on the key and appends the mapping line to the authfile
pamu2fcfg --origin=pam://$(hostname) --appid=pam://$(hostname) >> ~/.config/pam_u2f
```

then in `/etc/pam.d/login` **above** the unix auth line - and keep a password
or second admin session working until you have tested it:

```
auth sufficient pam_u2f.so origin=pam://<hostname> appid=pam://<hostname>
```

## PIV (experimental)

Needs `pynitrokey[pcsc]`, a running `pcscd` and the `--experimental` flag on
every command. The factory defaults are published (PIN `123456`, PUK
`12345678`, management key = the NIST key, see the PIN table) - replace them
before real use; commands taking the admin key default to the published one.
A blocked PUK only clears with a factory reset (see the factory reset
workflow).

```bash
nitropy nk3 piv --experimental init                        # initialize, prints the GUID
nitropy nk3 piv --experimental change-pin                  # prompts for current + new value
nitropy nk3 piv --experimental change-puk                  # prompts likewise
nitropy nk3 piv --experimental reset-retry-counter         # unblock a blocked PIN with the PUK
nitropy nk3 piv --experimental change-admin-key --current-admin-key <old-hex> <new-hex>
nitropy nk3 piv --experimental generate-key --key 9A --algo nistp256 --subject-name "CN=me" --path 9a.csr
nitropy nk3 piv --experimental write-certificate --key 9A --format pem --path cert.crt
nitropy nk3 piv --experimental list-certificates           # or read-certificate --key 9A
```

`get-windows-auth-mapping` prints the `altSecurityIdentities` string that maps
the card to a Windows AD user.

## Sources

- <https://docs.nitrokey.com/nitrokeys/nitrokey3>
- <https://docs.nitrokey.com/nitrokeys/nitrokey3/faq> - key counts, algorithms, secure element
- <https://docs.nitrokey.com/nitrokeys/nitrokey3/set-pins>
- <https://docs.nitrokey.com/nitrokeys/nitrokey3/reset> - raw APDU sequence
- <https://docs.nitrokey.com/nitrokeys/features/piv/access_control> - PIV PIN/PUK defaults
- <https://docs.nitrokey.com/nitrokeys/features/piv/key_management> - PIV key slots
- <https://github.com/Nitrokey/pynitrokey> - `pynitrokey/cli/nk3/piv.py` (default management key, factory-reset error), `pynitrokey/nk3/piv_app.py` (APDUs: PIN ref 0x80, PUK ref 0x81, reset INS 0xFB)
- <https://www.gnupg.org/documentation/manuals/gnupg26/gpg-card.1.html>
- <https://developers.yubico.com/pam-u2f> - pamu2fcfg registration and PAM setup
