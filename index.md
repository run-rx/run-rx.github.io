---
layout: home
title: Welcome
nav_order: 1
---

# rx supercharges your development environment

rx is a command-line tool to make ML development easy. It integrates with
whatever tools you're currently using and gives you a long-running VM in the
cloud that is kept in sync with your local machine.

* No ops required - just code and run. Machines are already configured and
  standing by.
* Long-running - your cloud environment persists between running commands. You
  can install packages, download models, and set up any other configuration
  you want.
* Private - your VM is fully isolated from everyone else's to maximize
  security and performance.

In the same way [Google Colab](https://colab.research.google.com/) lets you
have a notebook, pre-configured and running in the cloud, rx allows you to
have a full VM.

Check out the [getting started](/getting-started) guide to start using rx in
less than five minutes.

## What rx does

When you run rx it takes care of a bunch of configuration on your behalf:

* It creates a private hosted environment for your project in the cloud.
* It copies your source code into that environment.
* It installs any dependencies your project needs.

Then, every time you run a command, it automatically syncs local changes to
your cloud instance and syncs outputs back to your local machine. rx hosts
your environment on our own cloud instances, so you never have to worry about
setup or teardown.

*Note: the `rx` binary is a thin client and does not run commands on your local
machine: it sends them to your cloud instance and runs them there.*

Right now rx is free to use, so please give it a try and [let us know](mailto:eng@run-rx.com) what you think!

## Installation

Install via pip:

    pip install run-rx

rx also requires rsync to run, make sure you have it installed:

    which rsync

If not, check out [its website](https://rsync.samba.org/download.html) or your
favorite package manager to install.

## Usage

In the directory containing your project (often your git root), run:

    rx init

This will prompt you to log in (or create an account) and allocate a machine
in the cloud for you to use. Then it will copy your project from your local
machine to the cloud instance and install any packages that your project needs.

It may take several minutes to allocate a machine, copy your source code, and
install packages (depending on your project).

Once rx finishes initializing, you can run any command on your remote worker
by prefixing it with "rx":

    rx python my-script.py
    rx ps ax
    rx 'echo $PATH > my-path.txt'

Check out the [getting-started](/getting-started/) section for more examples.

## Feedback

Feel free to [file an issue](https://github.com/run-rx/rx/issues) if you have
any questions or problems!
