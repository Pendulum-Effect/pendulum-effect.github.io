---
title: "server sleds: a fixture plate that finally stopped the chatter"
date: 2026-07-19 10:15:00 -0500
categories: [server-sleds]
tags: [machining, aluminum, fixture, placeholder]
---

The milled-aluminum server sleds have always had one ugly step in the process: the second op. Flip the part, clamp on machined faces, and pray. The chatter marks on the last batch finally annoyed me into building a proper fixture.

## What was wrong

Second-op clamping was happening on two thin rails, which meant the part rang like a tuning fork on any cut near the middle. I'd been hiding it with lighter passes and a slower feed, which doubled cycle time and still left witness marks you could feel with a fingernail.

## The fixture

The v2 fixture is a flat plate with:

- Two dowel pins picking up holes that already exist in the sled's first op, so location is repeatable without indicating anything.
- Four low-profile clamps bearing on the thick corners instead of the rails.
- A relief pocket under the web so through-cuts never touch the plate.

The dowel-pin trick is the part I should have done a year ago. Op 2 setup went from ten fussy minutes with an indicator to drop-on, clamp, go.

## Results

Same tooling, same machine, but with the part actually supported: full-depth finishing passes, no chatter, and the cycle time for op 2 dropped by about 40%. The surface finish is good enough now that I'm tempted to skip the bead blast — although consistency across the batch probably still argues for it.

Next batch will tell whether the dowel holes wear. If they do, hardened bushings go in and this post gets a sequel.

*Fixture design was sketched with AI assistance; final dimensions and toolpaths verified in CAM before cutting.*
