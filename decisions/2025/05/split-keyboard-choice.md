---
slug: 2025-05-21-keyboard-decision
title: Choosing the Split Keyboard
date: 2025-05-21
status: accepted
tags: [decision, shopping, keyboard, hardware, vietnam]
impact: medium
---

I want a split, wired & wireless, ergonomic keyboard to improve my `Vim workflow` and reinforce proper `touch typing technique`.  
Given I'm in Vietnam, leading brands aren't available locally or would be slow/expensive to import.

<!-- truncate -->

---

## Post-Decision Review (2025-05-27)

After using the **Corne Split V4 Wireless Kit** for a few days, here are my observations:

### Positive:
- The split layout significantly reduces wrist strain during long typing sessions.
- The adjustable split design allows for better shoulder positioning, especially beneficial for users with wider shoulders.

### Negative:
- Bluetooth connectivity with my PC and Win 11 couple times has issues, didnt test in Linux yet.
- The **220mAh battery** lasts closer to 1 week with heavy use, not the claimed 4 weeks.

### Next Steps:
- Monitor the availability of **Kailh Choc 1350 switches** and keycaps for a potential upgrade.
- Consider adding external lighting or upgrading to a case with built-in backlighting in the future.

---

### Options Reviewed

- ✅ **Corne Split V4 Wireless Kit** — Supports both **Cherry MX** and **Kailh Choc 1350** switches via hotswap sockets (confirmed).
Choc switches not in stock now, but seller expects to restock within a week.
- ❌ **Sofle Kit** — Only supports Cherry MX, confirmed by seller. No low-profile support.

---

## Decision

I decided to buy the **Corne Split V4 Wireless Kit** with the dual-compatible PCB and hotswap sockets.  
I chose **Brown switches** (tactile, quiet) and **black/white keycaps** from the seller's current stock.  
Later, I plan to try **Kailh Choc 1350 switches** once they're available again.

The seller confirmed that:
- ✅ The PCB supports **both MX and Choc switches**
- ✅ **Hotswap sockets are installed**, so no soldering is required to swap switches
- ✅ Choc switches and keycaps will be available **soon** (expected next week)

---

## Components

What I Get vs What I Still Need

🧩 Included in Kit (₫1,488,000 | ~ USD 57 total, fully assembled)
- ✅ **Corne V4 PCB** with pre-soldered microcontroller and battery
- ✅ **nRF52840 chip** (Bluetooth 5.0 + USB-C wired support)
- ✅ **220mAh battery** (claimed ~4 weeks runtime)
- ✅ **3D-printed case**, plate, screws, stabilizers
- ✅ **Firmware compatibility** (QMK/VIAL)
- ✅ **Switch compatibility**: both Cherry MX and Choc 1350
- ✅ **Hotswap sockets installed**
- ✅ **Brown tactile switches** installed
- ✅ **Black/white keycaps** installed

❗ Optional Future Upgrades
- 🧩 **Kailh Choc 1350 switches** + keycaps (when back in stock)
- 🧩 **Tenting feet** for angled typing
- 🧩 **Bluetooth dongle** if onboard wireless proves unstable

---

## Consequences

**Positive:**
- Locally available, fast shipping
- Split layout promotes ergonomics and typing precision
- Fully assembled, plug-and-play with my chosen switches and caps
- Future support for low-profile switches
- QMK/VIAL programmable firmware

**Negative:**
- Still waiting for Choc switch stock
- No LED/backlight options
- Only one switch type per order (Choc must wait)

---

## Alternatives Considered

1. **Sofle Split Kit (₫2,090,000)**  
   - More keys, larger layout, acrylic case  
   - Rejected: No Choc support, more expensive, heavier

---

## Related

- `2025-05-21-typing-discipline.md` (planned)

---

## Notes

**Hotswap sockets** make it easy to change switches by hand — no soldering.  
This kit supports both **Cherry MX** (traditional) and **Kailh Choc 1350** (low-profile) switches, assuming matching keycaps are used.

When Choc parts are in stock:
- Remove Cherry MX switches with a switch puller
- Plug in Choc switches directly
- Replace keycaps with Choc-compatible ones

---

## References

- [Shopee Corne Kit Listing][shopee]
- [Shopee Sofle Kit Listing][sofle]
- [Detailed Build Log for Corne Keyboard][buildlog]

[shopee]: https://shopee.vn/B%C3%A0n-Ph%C3%ADm-Kit-Corne-Split-V4-Wireless-Bluetooh-H%E1%BB%97-Tr%E1%BB%A3-Choc-1350-Cherry-Mx-S%E1%BB%AD-D%E1%BB%A5ng-NRF52840-i.100162131.27722801716  
[sofle]: https://shopee.vn/product/19435042/10022249457
[buildlog]: https://github.com/rafaeldelboni/buildlogs/blob/main/crkbd-choco-v2.1.0.md

