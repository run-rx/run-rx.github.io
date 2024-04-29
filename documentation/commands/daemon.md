---
layout: page
title: daemon
permalink: /docs/commands/daemon
parent: Subcommands
grand_parent: Documentation
nav_order: 3
---

# daemon

Manages rx-daemon, which handles port forwarding. In general, you should not
need to interact with the daemon directly.

By default, the daemon listens on port 8478 and has a pid file stored in
_.rx/trex.run-rx.com/config/daemon.pid_. Logs are stored in
_$TMPDIR/rx-daemon.INFO_.

## start

Starts the daemon. You generally do not have to call this manually.

Example:

    rx daemon start

## stop

Stops the daemon.

Example:

    rx daemon stop

## info

Gets the daemon's pid, if it is running.

Example:

    rx daemon info
