---
slug: rpi-homelab-cluster
title: Initial Roles and Stack for RPi Cluster
date: 2025-06-13
status: accepted
tags: [decision, raspberrypi, matrix, infra, networking, todo]
impact: high
---

## Context

This cluster rebuild is part of a broader plan to enable home-staged development for Matrix-based
infrastructure (e.g. Danang Connect, TheArchitect). 4x RPi 4 and 2x RPi 5 are available, all PoE
powered via Gigabit switch.

<!-- truncate -->

## Decision

Assign initial roles for each Raspberry Pi device to cover essential services:

### RPI4 Devices (Fedora ARM)

- **RPI4-1:** Will later resume DHCP/DNS duties. Temporarily retired while ISP router handles it.
- **RPI4-2:** General-purpose Docker host for staging/dev environments
- **RPI4-3:** Matrix homeserver node for Synapse testing
- **RPI4-4:** Experimental host for federation, edge relay, or upcoming services

### RPI5 Devices (Raspberry Pi OS)

- **RPI5-1:** GUI admin node (Cockpit, Netdata, etc.) for overview/metrics
- **RPI5-2:** Matrix testbed with full stack (Synapse + Postgres + Redis + Element + widgets)

## Rationale

- Fedora ARM chosen for RPi4 to test systemd-native workflows, selinux support, and robustness
- Raspberry Pi OS kept for RPi5 for GUI and hardware support compatibility
- Will evolve into cluster-managed setup over time (possibly Kubernetes or Ansible automation)

## Consequences

- Short-term inconsistency in distros, but allows focused testing
- Some SD card churn expected if builds fail — keep backups of image/config
- Future work will involve automating provisioning and central logging/monitoring
