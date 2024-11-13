---
title: How to mount a LUKS RAID volume after a server reboot
categories:
  - Docs
tags:
  - Bash
  - Linux
---

Mounting a RAID assembly after a reboot requires three steps:

 1. Activate (run) the assembly
 2. Unlock the LUKS partition
 3. Mount the LUKS target to a directory

```bash
sudo mdadm --run /dev/md0
sudo cryptsetup open /dev/md0 lukstarget --type luks
# LUKS will prompt for a password and/or keyfile
sudo mount /dev/mapper/lukstarget /mnt/raid
```

This assumes you already have a RAID assembly created.
