---
layout: page
title: Environment
permalink: /docs/env/
parent: Documentation
nav_order: 4
---

# Remote machine environment

There are several standard features of the remote machine environment.

The user is root and your source code is uploaded to _/root/rx/app_. This is
called your rx root. Outputs under _/root/rx/app_ are synced back to your
local machine.

rx sets the the environment variable `IS_RX`. This allows scripts to check if
they're running under rx.

Your machine's hostname is initialized to the directory name of your rx root.

The environment variable `$TMPDIR` is set to _/root/scratch/tmp_ on the remote
machine.
