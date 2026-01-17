---
slug: bitwarden-ssh-agent
title: Bitwarden SSH Key Management
date: 2025-06-09
status: accepted
tags: [security, keyflow, ssh, bitwarden, decision, todo]
impact: medium
---

## Context

After my previous YubiKey broke and considering my specific needs — SSH and optionally sudo
authentication — I evaluated several approaches to secure key management. My key requirements were:

- No private keys stored in dotfiles or local disk
- Secure access to private keys without physical token dependency
- Optionally unlock sudo using something like challenge-response
- Maintain physical backup capability

This decision also comes in response to a past compromise where my SSH and GPG keys were leaked —
password-protected, but still required full regeneration.

<!-- truncate -->

### Next Steps

- [ ] Implement sudo authentication via `pam_exec` if needed
- [ ] Move gpg keys if possible
- [ ] Test disaster recovery procedures

## Post-Decision Update (2025-06-11)

After 1 day of real-world usage, several issues emerged:

- ❌ **Automount Limitation**: It's not possible to automount an encrypted USB. The drive must first
  be decrypted manually before it can be mounted — making the system inconvenient and error-prone
  during reboots or disconnections.
- ❌ **SSH Config Pitfalls**: Using `IdentityFile` paths inside the mounted vault introduced
  instability. Even arguments overwritten ssh key related options may attempt to access the key,
  freezing if the vault was not mounted. This behavior also triggered erratic responses from
  background SSH agents.

### Revised Strategy

My initial motivation was to:

- Avoid storing private keys in Git/dotfiles (past leak),
- Avoid re-entering passphrases repeatedly,
- Maintain physical backup.

Instead of using the encrypted USB drive as an **active vault**, I now:

- ✅ Store **private keys and passphrase directly in Bitwarden**.
- ✅ Avoid `IdentityFile` configs that point into dynamic mount locations.
- ✅ Use the encrypted USB flash drive as **cold backup only**, not active key source.
- ✅ Keep decryption/mount scripts on both server and client, for when manual access to backup is
  needed.

This eliminates runtime dependency on the USB vault and allows stable SSH operation with
Bitwarden-managed key access.

### Final Setup

- Server has manual scripts to decrypt and mount the USB vault as needed.
- Client has an SSHFS script to mount the vault when needed.
- Bitwarden provides seamless passphrase entry without needing the USB vault mounted.

#### SSH Configuration for Bitwarden Integration

1. Enable SSH agent in Bitwarden settings
2. Add to `~/.zshrc` or `~/.bashrc`:

   ```bash
   if [ -S "$HOME/.bitwarden-ssh-agent.sock" ]; then
     export SSH_AUTH_SOCK="$HOME/.bitwarden-ssh-agent.sock"
   fi
   ```

3. Configure `~/.ssh/config`:

   ```ini
   Host *
     PubkeyAcceptedKeyTypes +ssh-rsa
     SendEnv COLORTERM MOSH_WITH_JUMP

   Host github.com
     HostName github.com
     User git

   Host proxy.it-pal.net
     HostName 65.109.4.3
     User pilot
     IdentitiesOnly yes
     IdentityFile ~/.ssh/pilot.rsa.pub
   ```

Key points:

- Only `.pub` files are stored locally for identity reference
- `PubkeyAcceptedKeyTypes +ssh-rsa` ensures compatibility
- SSH agent socket delegation enables Bitwarden to manage key access
- `IdentitiesOnly yes` prevents fallback to other keys

---

## Post-Decision Update (2025-06-09)

Implementation completed with the following setup:

### Hardware

- Using 1GB USB drives (specially ordered) for key storage
- Currently using a 32GB drive temporarily while waiting for the smaller drives
- Raspberry Pi WAN as the host system

### Server-side Setup (Raspberry Pi)

1. LUKS encryption setup:

   ```bash
   sudo cryptsetup luksFormat /dev/sda
   sudo cryptsetup luksOpen /dev/sda secureusb
   sudo mkfs.ext4 /dev/mapper/secureusb
   sudo mount /dev/mapper/secureusb /mnt/secureusb
   ```

2. Auto-mount configuration:

   - Added to `/etc/crypttab`:
     ```
     secureusb UUID=4dddbcc9-da18-4021-b938-5690f979ef75 none luks,noauto
     ```
   - Added to `/etc/fstab`:
     ```
     /dev/mapper/secureusb /mnt/secureusb ext4 noauto,x-systemd.automount 0 2
     ```

3. Created dedicated `secureusb` user with SSH access (password + key authentication)

### Client-side Setup

1. Systemd user mount unit (`~/.config/systemd/user/home-this-secureusb.mount`):

   ```ini
   [Unit]
   Description=SSHFS mount of USB Vault
   After=network-online.target
   Wants=network-online.target

   [Mount]
   What=secureusb@raspberry-wan:/mnt/secureusb
   Where=%h/secureusb
   Type=fuse.sshfs
   Options=IdentityFile=%h/.ssh/secureusb_rsa,uid=%U,gid=%U,allow_other,reconnect,ServerAliveInterval=15,ServerAliveCountMax=3

   [Install]
   WantedBy=default.target
   ```

2. Enabled FUSE user mounting in `/etc/fuse.conf`:
   ```
   user_allow_other
   ```

In order to remount:

```
systemctl --user restart home-this-secureusb.mount
```

## Decision

I will build a USB-based SSH key vault using a USB flash drive, encrypted with LUKS and hosted on a
Raspberry Pi in local lan. The flash drive will contain my GPG and SSH private keys, which are not
stored anywhere else.

Access to the USB will be via SSHFS from my main laptop. A dedicated `vault` user will be created on
the host, configured with SSH password + key authentication. The client machine will mount the USB
via SSHFS and symlink or access key material directly.

To support **mobility**, I will maintain a second encrypted USB drive with a clone of the vault,
plugged directly into my laptop when away from the LAN.

For **off-site backup**, I will periodically upload an encrypted image of the USB to both:

- S3 backup bucket (object-locked, versioned)
- Google Drive (via `rclone` with encryption enabled)

Sudo authentication will remain password-based, but may be extended later using `pam_exec` to verify
the presence of a file or token on the mounted USB.

## Consequences

- ✅ SSH key is physically isolated and not on the local filesystem.
- ✅ Secure but inexpensive alternative to YubiKey for my specific needs.
- ✅ Sudo password remains as fallback; potential for `pam_exec` addition later.
- ✅ The key can be hosted remotely on LAN, or plugged directly when traveling.
- ✅ The encrypted USB is cloned and backed up to S3 and Google Drive for disaster recovery.
- ⚠️ Slight delay or manual step required to unlock and mount the drive.
- ⚠️ `vault` user on Pi must be secured and restricted (attack surface exists).
- ⚠️ SSHFS mount must succeed before anything requiring the key can proceed.

## Alternatives Considered (optional)

1. New YubiKey — secure and elegant, but ~$50 and overkill for now.
2. Local encrypted file — works, but less physically secure than USB.
3. SSH private key on a non-mounted USB — usable, but requires plugging in each time.
