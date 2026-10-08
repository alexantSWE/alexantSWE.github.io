---
title: "پشتیبان‌گیری خودکار با systemd timer"
date: 2026-10-05
tags: ["linux", "systemd", "backup"]
translationKey: systemd-backup-timer
---

اسکریپت پشتیبان‌گیری که فقط وقتی خودتان یادتان بیاید اجرا می‌شود، فایدهٔ چندانی ندارد. با یک systemd timer می‌شود آن را هر شب و بی‌سروصدا خودکار کرد.

<!--more-->

## اسکریپت

یک اسکریپت کوچک در `~/bin/backup-documents.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail
src="$HOME/documents"
dst="$HOME/backups/documents-$(date +%F).tar.gz"
mkdir -p "$(dirname "$dst")"
tar -czf "$dst" "$src"
```

## دو unit

فایل `~/.config/systemd/user/backup-documents.service`:

```ini
[Unit]
Description=Back up documents

[Service]
Type=oneshot
ExecStart=%h/bin/backup-documents.sh
```

فایل `~/.config/systemd/user/backup-documents.timer`:

```ini
[Unit]
Description=Run the documents backup nightly

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

## فعال‌سازی

```bash
systemctl --user daemon-reload
systemctl --user enable --now backup-documents.timer
systemctl --user list-timers
```

## نکته

گزینهٔ `Persistent=true` باعث می‌شود اگر سیستم هنگام زمان‌بندی خاموش یا در خواب بود، پشتیبان‌گیری در اولین فرصت بعدی اجرا شود. برای دیدن نتیجه، خروجی سرویس را بخوانید:

```bash
journalctl --user -u backup-documents.service
```
