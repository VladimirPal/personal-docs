---
slug: fedora-brave-bitwarden-2025-06-12
title: Brave Bitwarden on Fedora Workstation
date: 2025-06-12
tags: [fedora, keyflow, bitwarden, brave, note, todo]
status: final
---

This note documents the pain and setup process I went through to make **Bitwarden** work 
with **Brave** browser and **fingerprint unlocking** on **Fedora Workstation 42+**.

## Context

I installed Fedora Worksation 42 recently on T590 and rebuilt my key authentication and 
convenience flow from scratch.

My goals:
- Keep **Bitwarden as password manager**, locked by fingerprint
- Use **Brave** as the main browser with Bitwarden extension
- Have Bitwarden **auto-start** and work reliably with biometric unlock

<!-- truncate -->

---

## TODO: Auto-updates

Current status of auto-updates needs verification:

- Brave: Need to check if DNF auto-updates work reliably
- Bitwarden: AppImage doesn't auto-update by default

If auto-updates aren't working, I'll need to implement a solution that:

1. Periodically checks for updates using existing upgrade actions in scripts
2. Downloads and installs updates automatically
3. Sends desktop notifications about available updates
4. Optionally auto-restarts the apps after update

Potential implementation approaches:
- Systemd timer to run upgrade checks
- Desktop notification integration via `notify-send`
- Auto-restart hooks in the upgrade scripts

---


## Fingerprint Setup on Fedora

First, I needed to register my fingerprint in Fedora.

To do that, I ran:

```bash
fprintd-enroll
```

This prompts for your finger and stores it under your current user profile.

To verify:

```bash
fprintd-list $USER
```

---

## Brave install script

Simple wrapper around DNF with commands to install, uninstall, upgrade, etc.

```bash
~/.scripts/fedora/brave.sh install
```

This was straightforward. I used Brave's official repo. The script allows reinstalling or checking
version easily. Nothing tricky here.

---

## Bitwarden install script:

I wrote a full script at `~/.scripts/fedora/bitwarden.sh` to handle:

- Downloading the latest AppImage from GitHub
- Installing it to `~/.local/bin/`
- Creating `.desktop` launcher and icon
- Setting up **native messaging** to Brave browser
- Creating a small wrapper `desktop_proxy` because AppImage mounts to `/tmp/.mount_*`
- Enabling autostart
- Managing upgrades and uninstall

Biometric unlock _only works_ if the Bitwarden app was launched and has integration enabled.
So I needed to launch it on startup, persist configs, and make sure Brave can talk to it
through native messaging.

---

## Native messaging config

Bitwarden ships a native messaging JSON file for Firefox. Brave needs a separate one.


```json
{
  "name": "com.8bit.bitwarden",
  "description": "Bitwarden Desktop bridge for Brave",
  "path": "$HOME/.config/Bitwarden/bitwarden-desktop-native-messaging-host",
  "type": "stdio",
  "allowed_origins": [
    "chrome-extension://nngceckbapebfimnlniiiahkandclblb/"
  ]
}
```

The `path` is a shell script shim that launches the actual AppImage path dynamically.
Otherwise it fails due to `/tmp/.mount_*` instability.

Without this, Brave sees Bitwarden but can't talk to it.

---

## Fingerprint unlock

After all the wiring was done, I finally got fingerprint unlock to work _only_ when:

- Bitwarden is already running
- Integration is enabled in Bitwarden Desktop (`Settings > Options > Allow browser integration`)
- Brave is restarted
- Native messaging config is placed **manually**
- Fingerprint is registered and accessible through PAM

Also: Bitwarden requires one manual unlock via master password after login — **then** it will
start using fingerprint unlock for the session.

---

## Lessons

1. AppImages are not ideal for apps needing desktop integrations — but they work if scripted right.
2. Native messaging is fragile and needs precise paths.
4. I now unlock Bitwarden with fingerprint inside Brave via the browser extension.

---

## Outcome

✅ Bitwarden launches on login  
✅ Brave extension successfully unlocks the vault via fingerprint  
✅ Password autofill in browser works reliably without typing master password  
✅ All setup is repeatable via two scripts:

```bash
~/.scripts/fedora/brave.sh install
~/.scripts/fedora/bitwarden.sh install
```

---

## Appendix: Why Flatpak Bitwarden and Brave don't work with biometrics

I initially tried using the **Flatpak** versions of Bitwarden and Brave — seemed like a clean approach.
But they failed at two critical points:

1. **Biometric unlock** was broken.
2. **Browser integration** (via native messaging) didn't work.

Here's why.

### Flatpak sandbox limitations

Flatpak apps run in containers with limited access to the system:

- They **can't see the fingerprint service (`fprintd`)** unless explicitly granted
- They **can't access PAM modules** or `/run/`/`/dev` paths without elevated permissions
- They **can't write native messaging JSON files** into the browser config path 
(like `~/.config/BraveSoftware/...`)

### Bitwarden Flatpak doesn't request proper permissions

As of writing, the Bitwarden Flatpak:

- Does **not** request DBus access to `org.freedesktop.fprintd`
- Does **not** configure native messaging for Flatpak browsers
- Has no support for inter-sandbox messaging for AppImage/host browser

So while Bitwarden **shows** fingerprint options, they simply do nothing in Flatpak. Same for Brave.

### Could it work with the right configuration?

**Yes, in theory.** A properly configured Flatpak could work.

But currently, **none of that is implemented**. Which is why I switched to:

- RPM install of Brave (via DNF)
- AppImage of Bitwarden + manual integration

---

### Summary

| Feature                  | Flatpak version        | RPM/AppImage workaround   |
|--------------------------|------------------------|----------------------------|
| Biometric unlock         | ❌ Broken              | ✅ Works via fprintd & PAM |
| Browser autofill         | ❌ Broken              | ✅ Works via native messaging |
| Requires manual config   | ✅ Yes                 | ✅ Yes, but predictable     |

Flatpak is promising. But until upstream devs properly configure permissions and portals —
it's **not reliable for system-level tools like Bitwarden**.
