---
layout: page
title: Subcommands
permalink: /docs/commands/
parent: Documentation
nav_order: 2
---

# Subcommands

There are several subcommands that can come after "rx". These take precedence
over user commands, e.g., "rx init" will always run the init subcommand, not
an "init" binary on the remote host.

## init

Creates and sets up a new remote machine.

    $ rx init

Options:

* `--remote`: specifies a remote configuration file to use. See
  [config](/config) docs for more info.
* `--dry-run`: prints the files that will be uploaded, without actually
  uploading them.

Running `rx init` a second time in a directory will shut down the current
remote machine and start a new one from scratch.

## run

This is the default command if nothing else is specified. It runs a command on the existing remote worker.

    $ rx run ls
    $ # Equivalent to:
    $ rx ls

It is only necessary to explicity use the `run` subcommand if you're running
a binary with the same name as another rx command. For example:

    $ rx run version  # Runs a binary called "version" on the remote

## version

Prints the current version.

    $ rx version
