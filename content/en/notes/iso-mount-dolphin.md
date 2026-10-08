---
title: "Mounting ISOs from the Dolphin context menu"
date: 2026-10-01
tags: ["kde", "python", "iso"]
translationKey: iso-mount-dolphin
---

I needed an ISO one day and noticed Dolphin has no mount option at all. Nautilus does this, so why not Dolphin?

<!--more-->

## The problem

There was no simple way from inside the file manager. Mounting from the terminal works, but typing it out for every file gets old fast.

## The fix

A context-menu entry was added that takes the ISO file and mounts it automatically:

```bash
udisksctl loop-setup -f "$1"
udisksctl mount -b /dev/loop0
```

The whole project lives in the [iso-mount-kde](https://github.com/alexantSWE/iso-mount-kde) repo.

## Note

If the mount doesn't come back, check `dmesg | tail` first — the problem is usually the loop device, not the file itself.
