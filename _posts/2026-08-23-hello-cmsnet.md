---
title: "Hello — what CMSNet is, and why this log exists"
date: 2026-08-23 12:00:00 -0500
categories: [meta]
tags: [cmsnet, homelab]
pin: true
---

CMSNet is my homelab: a ZimaOS core, UniFi networking, and a slowly growing
family of custom-built hardware around it — an ESP32 status display, a rack of
milled-aluminum server sleds, and now a custom carrier board. This log is the
public subset of my lab notebook: what I tried, what broke, what fixed it.

Two ground rules for this site:

1. **Lab notes, not articles.** Entries are written for the next person who
   hits the same problem (often future me). Expect rough edges.
2. **Credit where due.** Much of this work stands on open-source projects and
   AI-assisted tooling. Each project repo carries its own attribution; when a
   post builds on someone's work, it's named in the post.

## The projects

| Repo | What it is |
| --- | --- |
| [zima-tinyscreen](https://github.com/Pendulum-Effect/zima-tinyscreen) | Flask/Docker app + ESP32-S3 firmware driving a front-panel AMOLED with live ZimaOS stats |
| mu-poe-carrier | PoE-powered LattePanda Mu carrier board for a ZimaOS server sled (fork of BenMakesEverything's Mu_Cyberdeck) |
| Gamekey sled system | Milled 6061 rack sleds in a UniFi AI-Key aesthetic — design notes will land here |
