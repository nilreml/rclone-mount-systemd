# rclone-mount-systemd

A [systemd](https://wiki.archlinux.org/title/systemd) [user service](https://wiki.archlinux.org/title/Systemd/User) template to automate mounting remote file systems using [rclone](https://rclone.org/).

## Overview

The service template will use the same `[remote]` name you specified when using [rclone config create](https://rclone.org/commands/rclone_config_create/).

Each remote will be mounted in `~/mnt/[remote]` (created automatically).

To avoid confusion, mounting will fail if the mount point isn't empty.

## Preparation

If you are using a desktop environment:

Add `user_allow_other` to `/etc/fuse.conf` if not already there (this requires root privileges).

## Install

Place `rclone@.service` in `~/.config/systemd/user/`.

> NOTE: The filename must include the `@`, e.g. `rclone@.service`

As your normal user, run

```sh
systemctl --user daemon-reload
```

## Usage

You may now start/enable each rclone remote by using `rclone@[remote]`

```sh
systemctl --user enable --now rclone@dropbox
```

## Tips

If you encounter the service ceasing to function when exiting the last session of ssh or not starting during boot, run

```sh
loginctl enable-linger [user]
```

## Attribution

Credits to Amy Nagle and the discussion contributors in [this very helpful GitHub gist](https://gist.github.com/kabili207/2cd2d637e5c7617411a666d8d7e97101).
