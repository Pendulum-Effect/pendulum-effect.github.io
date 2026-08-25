---
title: "zimaos core: running the restore drill I kept postponing"
date: 2026-08-02 20:45:00 -0500
categories: [zimaos-core]
tags: [zimaos, backup, restore, placeholder]
---

A backup you've never restored is a rumor, not a backup. This week I finally scheduled the drill: pretend the ZimaOS core died, and rebuild it from what the backups actually contain — not from what I remember being on it.

## The scenario

Rules of the drill: fresh install on spare media, no peeking at the live system, and everything has to come back from the documented backup set plus the runbook in the private notebook. If I had to SSH into the live box to check how something was configured, that counted as a documentation failure and went on the fix list.

## What broke

The data all came back clean — the snapshot discipline is working. What failed was the boring glue:

- Two services referenced storage paths that only existed because I'd hand-created them ages ago. The runbook never mentioned them.
- A container env file lived outside the backed-up config tree. It's inside now.
- The restore doc said "reconfigure networking" with zero detail. Thanks, past me. It now has actual steps, still with nothing sensitive in the public half.

## The score

Call it a B-minus: data 10/10, config 7/10, documentation 5/10. Total time from blank media to all services green was an afternoon, most of it spent rediscovering the glue. The fix list is short and all of it is documentation.

Next drill in six months, and the calendar entry is already made — because the entire lesson of this one is that "I'll remember" is not a system.

*Runbook cleanup was done with AI assistance; all restore steps were executed and verified by hand.*
