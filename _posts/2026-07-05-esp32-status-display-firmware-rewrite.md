---
title: "esp32-status-display: rewriting the firmware around a draw queue"
date: 2026-07-05 14:30:00 -0500
categories: [esp32-status-display]
tags: [esp32, firmware, display, placeholder]
---

The ESP32 status display has been running the same spaghetti loop since v1: poll everything, redraw everything, block on Wi-Fi, repeat. It worked, but every added stat made the refresh visibly jankier. Time to pay the debt.

## The problem

The old loop redrew the entire panel every cycle, even when nothing changed. On an SPI display that means a full-frame push every second, and the polling calls sat inline with the drawing — so a slow HTTP response froze the whole screen mid-render. Classic first-draft firmware.

## The new structure

The rewrite splits things into three pieces:

- **Collectors** run on a timer and write into a shared state struct. Each one owns its own retry/backoff, so a dead endpoint just goes stale instead of stalling the UI.
- **A dirty-flag draw queue** compares incoming state to what's on screen and only redraws regions that changed.
- **The render task** drains the queue at a fixed cadence, so the display refresh cost is bounded no matter how chatty the collectors get.

```cpp
struct PanelState {
  float cpu_pct;
  float mem_pct;
  uint32_t uptime_s;
  bool stale;
};
```

Nothing here is novel — it's the pattern every embedded UI eventually converges on — but the difference on the panel is dramatic. Updates land in under a frame, and a flaky endpoint now shows a little stale-data glyph instead of freezing the clock.

## What's next

Backlight scheduling (the thing is a lighthouse at 2 AM), and maybe a second page cycling on a physical button. The button is already wired; the debounce code is already embarrassing.

*Portions of this firmware were developed with AI assistance; all code is reviewed and tested on hardware before deployment.*
