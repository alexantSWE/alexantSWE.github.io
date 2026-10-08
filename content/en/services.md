---
title: "What I can help with"
description: "Practical technical help for Linux, operating systems, software, and repetitive work."
---

My work is closest to a **technical handyman**: something is not working, a process has become too manual, or nobody knows where an error began. I focus on the general state of software and operating systems rather than specialist support for one particular application.

## Linux and system setup

From choosing a distribution and installing it to partitioning, drivers, dual boot, and the first useful setup. The point is not only to get a system to boot, but to make it genuinely ready to use.

## System and software troubleshooting

For things such as:

- A system that will not boot or suddenly feels slow
- Broken packages and dependencies
- An app that refuses to launch and has an unhelpful error message
- Network, permission, or configuration problems after a change or update

I usually start with the simplest signals and the logs—for example, `systemctl`, `journalctl`, and `dmesg` on Linux.

## Automation and scripting

If work repeats every day or every week, it can probably get shorter. Small Bash or Python scripts can make backups, organize files, batch-convert them, or run a repeatable sequence of commands.

```bash
#!/usr/bin/env bash
# example: back up a folder
set -euo pipefail
tar -czf "backup-$(date +%F).tar.gz" "$1"
```

## Configuration and customization

Configuration files, terminals, keyboard shortcuts, window managers, and dotfiles: anything that helps a system better fit the way you work.

## Backups, files, and disks

I can help set up a backup routine, organize files, resolve access problems, or take a first look at disk and partition issues. For important data, preserving the original and reducing risk always comes first.

## Small but stubborn jobs

An ISO that will not mount from the context menu, a stuck update, a missing menu item, or a configuration file where one line broke everything. These are often the jobs that take far more patience than they should.
