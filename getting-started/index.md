---
layout: page
title: Getting Started
permalink: /getting-started/
has_children: true
nav_order: 2
---

# Getting started guide

Welcome to rx! This section contains a series of examples to demonstate using
rx. To get started, create a directory to use for this tutorial and set up
a virtual environment:

    $ mkdir getting-started
    $ cd getting-started

Install rx by running:

    $ pip install run-rx

See the [install section](/docs/install) if you need more info.

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
