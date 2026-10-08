---
title: "مونت نشدن ISO در منوی راست‌کلیک Dolphin"
date: 2026-10-01
tags: ["kde", "python", "iso"]
translationKey: iso-mount-dolphin
---

روزی به یک ISO نیاز داشتم و دیدم فایل‌منیجرم (Dolphin) هیچ گزینه‌ای برای mount کردن ندارد. Nautilus این کار را می‌کند، پس چرا Dolphin نکند؟

<!--more-->

## مشکل

هیچ راه ساده‌ای از داخل فایل‌منیجر نبود. mount از ترمینال جواب می‌دهد اما هر بار تایپ کردن آن برای هر فایل حوصله‌سربر است.

## راه‌حل

یک ورودی به منوی راست‌کلیک اضافه شد که فایل ISO را می‌گیرد و به‌صورت خودکار mount می‌کند:

```bash
udisksctl loop-setup -f "$1"
udisksctl mount -b /dev/loop0
```

کل پروژه در مخزن [iso-mount-kde](https://github.com/alexantSWE/iso-mount-kde) است.

## نکته

اگر mount به درستی برنگشت، اول `dmesg | tail` را ببینید — معمولاً مشکل از loop device است، نه از خود فایل.
