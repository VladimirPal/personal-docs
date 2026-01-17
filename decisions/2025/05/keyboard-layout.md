---
slug: 2025-05-28-keyboard-layout-decision
title: Designing Personal Keyboard Layouts for ZMK
date: 2025-05-28
status: active
tags: [decision, keyboard, zmk, layout, productivity, vim, ergonomics, firmware]
impact: high
---

## Context

After acquiring the **Corne Split V4 Wireless** keyboard, I’m beginning the process of designing my own **custom ZMK layouts**.  
This is expected to evolve over time — similar to how `.vimrc` or `.zshrc` never really stop growing.

However, I’m **not aiming for perfection** from day one. My top priority is to unblock my daily coding and writing workflows by restoring essential symbols (`^`, `.`, etc.) and testing layer switching. Fancy ideas can wait.

This will also be my **first time flashing ZMK firmware**. Gaining hands-on experience with the flashing process is part of the goal.

<!-- truncate -->

---

## Current Setup

- **Keyboard**: Corne Split V4 Wireless
- **Firmware**: ZMK (via Web Keymap Editor)
- **Repo**: [`VladimirPal/Corne-OLED_Wireless`](https://github.com/VladimirPal/Corne-OLED_Wireless)
- **Source**: Forked from the seller’s repo (contains the current default layout)
- **Switches**: Cherry MX Brown (temporary — planning to switch to Choc 1350)
- **Layers**:
  - `default_layer`: QWERTY base with Vim and coding keys
  - `lower_layer`: Numbers, arrow keys, BT switching
  - `raise_layer`: Symbols and punctuation

---

## Goals

Immediate, practical goals:

- **Add missing key symbols** (e.g. `^`, `.`, `~`)
- **Upload and test firmware** with these layout changes
- **Keep all default functionality intact** (BT switching, media keys)
- Use the experience to validate the build+flash process

Future/iterative goals:

- Create a **Vim-optimized layer**
- Use **tap dance**, **hold-tap**, and **one-shot mods** wisely
- Build a **clean mental model** with 3–4 predictable layers
- Store layouts in a versioned repo and document rationale in `CHANGELOG.md`

---

## Challenges

- First-time flashing: risk of breaking something temporarily
- Wireless layer switching latency may affect experience
- Adjusting to split layout is still ongoing (slower typing speed)
- Not enough time to explore advanced behaviors (for now)

---

## Decision

- Proceed with **incremental edits** to the default layout (add missing symbols, test layers)
- Use [Web Keymap Editor](https://nickcoutsos.github.io/keymap-editor/) with the connected GitHub repo
- Flash firmware and validate that:
  - All layers behave as expected
  - Critical symbols are available
  - BT switching and navigation keys work

This is not the final layout — it’s just the **first snapshot** in a longer, documented evolution.

---

## Consequences

**Positive:**
- Essential symbol keys restored for daily productivity
- Layout is ready for real use, with all default features preserved
- Flashing experience gained
- A clear base from which future tweaks can evolve

**Negative:**
- Potential for time spent debugging flashing or broken bindings
- May slowly drift into endless iteration (like dotfiles) if not scoped clearly

---

## Related

- `2025-05-21-keyboard-decision.md`
- `2025-05-21-typing-discipline.md` (planned)

---

## Notes

This decision anchors a **practical starting point**.  
The goal is not optimization but utility — I can’t work efficiently if I’m missing basic characters.  
Once this baseline is stable, I’ll revisit the idea of a Vim layer and ergonomic refinements.

idea: tri-layer emoji layout  
idea: hold f switch on layer where keys tap goes with ctrl combo in order to move betwen tabs.
