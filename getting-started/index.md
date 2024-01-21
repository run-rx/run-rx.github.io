---
layout: page
title: Getting Started
permalink: /getting-started/
has_children: true
nav_order: 2
---

# Getting started guide

Welcome to rx! rx makes it easy to set up, use, and share a remote environment
while letting you continue to use all of your favorite local tools.

The getting started guide provides interactive examples to get you familiar with
rx. To begin, create a directory to use for this tutorial:

    $ mkdir getting-started
    $ cd getting-started

Install rx by running:

    $ pip install run-rx

See the [install docs](/docs/install) for more info.

Finally, get this directory mirrored on a remote machine by initializing it
with rx:

    $ rx init

This sets up rx in the current directory, similar to "git init". It will
prompt you to log in and/or create an rx account. Then it will set up a
machine for you in the cloud and copy over any local files (although there
aren't any yet).

Now you're ready to get started with
[hello world](/getting-started/hello-world).

The full code for this section is also available in the
[getting-started](https://github.com/run-rx/getting-started) repository on
GitHub, if you prefer to clone that and run the finished examples.
