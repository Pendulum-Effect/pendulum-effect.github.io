---
title: "mu-poe-carrier: forking a cyberdeck into a PoE server sled (schematic v02)"
date: 2026-08-23 14:00:00 -0500
categories: [mu-poe-carrier]
tags: [lattepanda-mu, poe, kicad, zimaos, usb-c]
image:
  path: /assets/img/posts/mu-poe-carrier/cover.jpg
  alt: "Stylized PCB routing graphic for the mu-poe-carrier v02 schematic"
---

The goal: a LattePanda Mu server sled for the rack that powers entirely over
802.3bt PoE and runs ZimaOS headless. Rather than designing a carrier from
scratch, I forked [BenMakesEverything's Mu_Cyberdeck](https://github.com/BenMakesEverything/Mu_Cyberdeck)
carrier (GPL-3.0, itself derived from DFRobot's reference design) — which
contributed the hard part: a proven SODIMM footprint and high-speed routing.

## What changed

- **Deleted:** PCIe x4 slot, barrel jack, all USB-A, M.2 E-key (WiFi), battery-era power path
- **Added:** 802.3bt Type 4 PoE input (Silvertel Ag5800 → 12 V), USB-C PD bench input
  (CH224K @ 15 V — amusingly, the donor board had this section fully designed but
  unpopulated, already strapped for 15 V), and an all-Type-C rear panel:
  USB-C 3.2 Gen1 via HD3SS3220 + USB-C 2.0 + PD-in
- **Kept:** HDMI for crash-cart debug, fan/thermal circuits, front-panel USB2 headers
  (one feeds the [zima-tinyscreen](https://github.com/Pendulum-Effect/zima-tinyscreen) AMOLED in the faceplate)

## Findings worth recording

1. **The donor's entire Gigabit Ethernet section was DNP** — schematic present
   (from the DFRobot reference), never populated or tested. If you're building
   on Mu_Cyberdeck and need Ethernet, treat that block as unproven.
2. **Don't double the USB3 AC coupling caps.** The donor already series-couples
   SSTX host-side (100 nF); inserting a mux and adding "reference design" caps
   would put two in series → 50 nF effective, below the USB spec window.
3. **5 V budget math matters when you advertise current.** One SY8253 (3 A) has
   to cover both USB-C ports + tinyscreen + spare header. Advertising 1.5 A on
   both ports oversubscribes it on paper; the fix was dropping the peripheral
   port to the 500 mA default.

## State

Schematic v02 done, nothing fabricated yet. Next: physical part selection
(bt MagJack, receptacles, load switches), then full PCB re-layout to 120 × 80 mm.
Board files and the complete engineering changelog live in the project repo.

*Schematic rework was AI-assisted (Claude); architecture, requirements, and
integration decisions — and the mistakes — are mine.*
