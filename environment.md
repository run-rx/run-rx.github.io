---
layout: page
title: Environment
permalink: /env/
---

There are several standard features of the remote machine environment.

The user is root and your source code is uploaded to _/root/rx/app_. Files
under _/root/rx/app/rx-out_ are synced back to the client, and a best-effort
attempt is made to sweep all outputs under _/root/rx/app_ to the client.

rx sets the the environment variable `IS_RX`, in case you need to check from
scripts if you're running remotely.

Your machine's hostname is initialized to the directory name of your rx root.

# Log files

Locally, logs are stored in Python's