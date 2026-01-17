---

slug: arch-via-fedora
title: Arch Linux installation via Fedora Live
date: 2025-08-04
tags: [arch, fedora, note]
status: draft
-------------

## 📌 Context

Due to a locked Secure Boot configuration with no way to enroll my own keys, the typical Arch Linux
installation with unsigned bootloaders will fail.

To bypass this, I:

* boot into **Fedora Live USB** (which is Secure Boot signed)
* install Arch from scratch to the disk using the **Arch bootstrap tarball**
* use **PreLoader.efi + HashTool.efi** to manually enroll hashes of unsigned binaries like
  `systemd-boot` and the kernel

The install script performs the installation using manual mount points and EFI manipulation.

---

## 🔧 Disk layout assumptions

| partition | mount point   | format | purpose                       |
| --------- | ------------- | ------ | ----------------------------- |
| p1        | `/boot` (ESP) | fat32  | EFI System Partition          |
| p2        | `/` (root)    | ext4   | Linux root filesystem         |
| p3        | `/mnt/tools`  | ext4   | temporary space for bootstrap |

Environment variables:

```bash
disk="/dev/nvme0n1"
esp="${disk}p1"
root="${disk}p2"
tools="${disk}p3"
```

---

## 🖥️ Mount points

| path             | purpose                                             |
| ---------------- | --------------------------------------------------- |
| `/mnt/root`      | Arch root system                                    |
| `/mnt/root/boot` | ESP mounted inside chroot (bootloader + kernel)     |
| `/mnt/boot`      | ESP mounted outside chroot for manual file copying  |
| `/mnt/root/efi`  | ESP mounted for `bootctl --esp-path=/efi` in chroot |

---

## ⬇️ Bootstrap workflow summary

1. **unmount and clean**: ensure no residual mounts.
2. **format partitions**: ESP (fat32) and root (ext4).
3. **mount root and esp** under `/mnt/root` and `/mnt/root/boot`.
4. **download PreLoader.efi + HashTool.efi** into tools partition.
5. **download and extract Arch bootstrap** into `/mnt/root`.
6. **bind system dirs**: `/dev`, `/proc`, `/sys`, `/run`.
7. **install base system** using `pacman` inside bootstrap.
8. **write fstab**, set hostname, configure networking.
9. **create user and root credentials**.
10. **install and configure systemd-boot** using `bootctl --esp-path=/boot`.
11. **copy PreLoader + HashTool into `EFI/systemd/` on ESP**.
12. **rename `systemd-bootx64.efi` → `loader.efi`** on ESP.
13. **create EFI boot entry manually with `efibootmgr`** pointing to PreLoader.
14. **on first boot**: use `HashTool.efi` to enroll:

    - `\EFI\systemd\loader.efi`
    - `\vmlinuz-linux`

---

## 🔎 Notes

- The bootloader is renamed to `\EFI\systemd\loader.efi` to be stable across updates and used by
  PreLoader.
- The kernel and initramfs are installed directly into the ESP root (`/boot/vmlinuz-linux`,
  `/boot/initramfs-linux*.img`).
- Only two ESP paths need enrollment in HashTool: `loader.efi` and `vmlinuz-linux`.
- Running this from a **Fedora live environment** works because Fedora is signed with Microsoft’s
  UEFI keys.
- **Kernel updates** require re-enrollment of `\vmlinuz-linux`.
- **Systemd updates** may update `systemd-boot`; re-enroll `\EFI\systemd\loader.efi` if so.
- A pacman hook (`warn-enroll`) is used to show desktop + journal notifications when either changes.

---

## 📖 Reference

- [PreLoader + HashTool blog](https://blog.hansenpartnership.com/using-efi-secure-boot-without-a-microsoft-signed-loader/)
- [Arch Linux bootstrap tarball archive](https://archive.archlinux.org/iso/)

---

## ✅ Final step reminder

After installation and reboot, manually enroll via `HashTool.efi`:

- `\EFI\systemd\loader.efi`
- `\vmlinuz-linux`

Without this step, Secure Boot will block the loader.
