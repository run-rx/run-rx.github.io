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

## help

Print help about the available commands.

Run `rx help <subcommand>` to see a specific command's help info.

## init

Creates and sets up a new remote machine.

    $ rx init

Options:

* `--remote`: specifies a remote configuration file to use. See
  [config](/config) docs for more info.
* `--dry-run`: prints the files that will be uploaded without actually
  uploading them.
* `--quiet`: by default, `rx` is very chatty and asks the user to confirm
  that they want to proceed after each step. If you have used `rx` before
  you can use `--quiet` to skip all the confirmations.

Running `rx init` a second time in a directory will shut down the current
remote machine and start a new one from scratch. This is essentially a wipe
back to the base state for your machine.

## run

This is the default command if another subcommand isn't found. It runs a
command on the existing remote worker.

    $ rx run ls
    $ # Equivalent to:
    $ rx ls

It is only necessary to explicity use the `run` subcommand if you're running
a binary with the same name as another rx command. For example:

    $ rx run version  # Runs a binary called "version" on the remote

## stop

This will stop the current machine you're using. This stores your current work
so you can pick it up on a new machine by simply running any command from your
workspace.

For example, suppose you create a file with `rx touch foo` and then shut
down the worker with `rx stop`. You can then run any command (e.g., `rx ls`)
and rx will provision a new worker with your saved state:

    $ rx ls
    Error syncing code to your worker, checking with the scheduler...
    Your workspace was stowed, please stand by while it is set up on a new machine.
    .......
    Done! Please rerun this command to use your newly restored workspace.
    $ rx ls
    foo

## subscribe

This will open a browser window and take you through creating a subscription.
Subscriptions are charged monthly with a base rate for unlimited CPU usage and
an hourly rate for GPU usage. You can cancel anytime from the command line
(see the `unsubscribe` command, below).

See the [pricing page](https://www.run-rx.com/pricing) page for more info on
subscriptions.

## unsubscribe

This will cancel your subscription and delete all of your data from rx's
machines. You will receive a final bill via email with any outstanding usage
in the current month.

## version

Prints the current version of the client you're using.

## workspace-info

Gets info about your current workspace. This returns a yaml config of the
workspace for this rx root, plus all commands you've run this month.
