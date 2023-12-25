---
layout: page
title: Output
permalink: /docs/output/
parent: Documentation
nav_order: 6
---

# Handling output files

When a command completes, rx copies the state of your remote rx root to your
local rx root. For example, suppose you start with a directory with just one
file, _hello_, in it:

    $ ls
    hello

If you create a new file remotely, rx will let you know it was created and
copy it to your local machine:

    $ rx touch world
    Changed:
      world
    $ ls
    hello    world

You can also remove files remotely and have that reflected locally:

    $ rx rm hello
    Changed:
      hello
    $ ls
    world

Note that rx copies the local state to the remote machine at the beginning of
each command, so running multiple long-running commands can yield inconsistent
remote states. Similarly, the remote machine writes its state back to the local
rx root when the command finishes executing.
