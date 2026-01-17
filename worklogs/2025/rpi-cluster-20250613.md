---
slug: worklog-rpi-cluster-2025-06-13
title: Worklog - Raspberry Pi Cluster for Lan Matrix-based Lab
date: 2025-06-13
tags: [worklog, deep, raspberrypi, infra, networking, matrix, homelab, todo]
---

# Deep Work Rebuild: Raspberry Pi Cluster for Lan Matrix-based Lab

## Session Length

8 p.m. – \~2 a.m. (6 hours with breaks) — intentionally \[deep]

---

## ❖ Goal

Rebuild all Raspberry Pi devices for use in a Matrix development lab, including physical rack
mounting, clean OS installs, network reconfiguration, and initial service layout for testing/staging
environments (e.g. Danang Connect).

<!-- truncate -->

---

## ✅ Phase 1: Physical Setup — COMPLETED

- Mounted all 6 RPis in 2 racks
- Verified working status of each board (booted Raspbian)
- Labeled units and placed in clean, accessible layout
- Reorganized cables, power, and PoE
- Noted: only 3 available PoE Type-C connectors → need to purchase 5 more
- PoE splitters placed **behind mosquito-trap fan** to allow passive cooling

Notes:

- Took longer than planned, but milestone is solid.
- Chaos on bed and table now represents temporary entropy. Acceptable.
- Cleanup will be needed soon. Optimization of wire length and airflow planned later.

## Next Suggested Step

➡️ Phase 2: Burn OS images + temporary DHCP/DNS reconfig

- \[shallow] Burn Fedora to RPi4s
- \[shallow] Burn Raspberry Pi OS to RPi5s (GUI if desired)
- \[shallow] Move DHCP/DNS to ISP router

---

## ❖ Task Plan

### Phase 1: Physical Setup

- \[deep] Physically mount all 6 RPis in 2 racks
- Label units:

  - RPI4-1 to RPI4-4
  - RPI5-1, RPI5-2

- Plug in PoE splitters + Gigabit switch

### Phase 2: Restore Baseline LAN

- \[shallow] Move DHCP/DNS temporarily back to ISP router (1st floor)
- \[maybe-deep] Log: consider replacing router with another Pi or low-power x86 box

### Phase 3: Burn OS Images

- \[shallow] Burn Fedora ARM to 4x RPi4 SD cards
- \[shallow] Burn Raspberry Pi OS to 2x RPi5 SD cards (enable GUI on 1 or both)
- \[maybe-deep] Shared boot config tweaks or pre-script setup (e.g. SSH keys, Wi-Fi backup)

### Phase 4: Role Planning (Initial)

- RPI4-1 → DHCP/DNS server (reclaim from ISP router later)
- RPI4-2 → Docker dev + staging
- RPI4-3 → Matrix homeserver (testing)
- RPI4-4 → Federation / experimentation
- RPI5-1 → Admin GUI (Cockpit, etc.)
- RPI5-2 → Matrix + Docusaurus + GPT bot testbed

### Phase 5: Network & Remote Access

- \[deep] Create stable tunnel from home LAN to external VPS
- \[maybe-deep] Consider Tailscale or WireGuard if SSH tunnel proves fragile
- \[maybe-deep] Setup `.home.arpa` or similar internal LAN DNS

### Phase 6: Matrix App Testbed

- \[deep] On RPI5-2:

  - Synapse + Redis + Postgres
  - Element Web or Element Desktop
  - widgets, Docusaurus site, TheArchitect bot

- \[maybe-deep] Automate this into a deploy script (Ansible or Bash)

### Optional: Daily Quick Wins

- \[shallow] Check CPU temp/load via SSH
- \[shallow] Run `nmap` to see live Pi IPs
- \[shallow] Log tunnel uptime

---
