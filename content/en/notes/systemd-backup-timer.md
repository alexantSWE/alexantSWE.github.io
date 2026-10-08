---
title: "Automatic backups with a systemd timer"
date: 2026-10-05
tags: ["linux", "systemd", "backup"]
translationKey: systemd-backup-timer
---

A backup script that only runs when you remember it is not worth much. A systemd timer can run it quietly, every night, on its own.

<!--more-->

## The script

A small script at `~/bin/backup-documents.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail
src="$HOME/documents"
dst="$HOME/backups/documents-$(date +%F).tar.gz"
mkdir -p "$(dirname "$dst")"
tar -czf "$dst" "$src"
```

## Two units

`~/.config/systemd/user/backup-documents.service`:

```ini
[Unit]
Description=Back up documents

[Service]
Type=oneshot
ExecStart=%h/bin/backup-documents.sh
```

`~/.config/systemd/user/backup-documents.timer`:

```ini
[Unit]
Description=Run the documents backup nightly

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

## Enable it

```bash
systemctl --user daemon-reload
systemctl --user enable --now backup-documents.timer
systemctl --user list-timers
```

## Note

`Persistent=true` means that if the machine was off or asleep at the scheduled time, the backup still runs at the next opportunity. To see the result, read the service log:

```bash
journalctl --user -u backup-documents.service
```
