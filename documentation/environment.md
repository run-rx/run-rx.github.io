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

rx sets the the environment variable `IS_RX`, in case you need to check from
scripts if you're running remotely.

Your machine's hostname is initialized to the directory name of your rx root.

## Temporary directory

The environment variable `$TMPDIR` is set to /root/scratch/tmp on the remote
machine.
