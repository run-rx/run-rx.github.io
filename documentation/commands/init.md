---
layout: page
title: init
permalink: /docs/commands/init
parent: Subcommands
grand_parent: Documentation
nav_order: 1
---

# init

Creates and sets up a new remote machine.

    $ rx init

By default, `init` will sync the contents of your current directory to the
remote host. If you'd like to see which files will be synced you can
run with `--dry-run`, which will print the files-to-be-uploaded and exit.

When you initially run `rx init`, it will create a default _.rxignore_ file
with some standard paths. You can modify this or create your own, then check
your work with `--dry-run`.

## Remote machine setup

By default, rx will examine your project and attempt to determine what
languages/tools you're using, then set them up on the remote machine. For
example, if you have a _requirements.txt_ file, rx will make sure Python is
installed on the machine and run `pip install` on your project. If your project
has a _package.json_ file, rx will install node and run `npm install` (and so
on).

This auto-detected toolchain is written to a file in _.rx/remotes/_, which
_.rx/remotes/default_ will automatically be symlinked to. When you run
`rx init`, it first checks for _.rx/remotes/default_ and will use that
(if it exists) instead of auto-detecting your setup.

## Using a custom remote configuration

You can create your own [custom configuration](/docs/config) and then
either symlink _.rx/remtoes/default_ to that file or use the `rx init`
option `--remote`. For example:

    rx init --remote=path/to/my-config.yaml

## Working purely remotely

If you'd like to work on code that does not exist on your machine, you can
pass in `--sync=false`. This will prevent rx from syncing files to/from your
local machine, but still allow you to use rx commands to work with the remote
workspace.

To specify the project to load on the remote machine, specify `--git`:

    rx init --sync=false --git=https://github.com/ashadnasim52/sentiment-analysis.git

You can also (optionally) specify the commit you wish to load the project at:

    rx init --sync=false \
      --git=https://github.com/ashadnasim52/sentiment-analysis.git \
      --commit=c93fd945f5a6a804f6db35ab2b98c34384de2c92

`--commit` defaults to HEAD.

Note that you can still configure a no-sync workspace with a `--remote` config.

## Re-creating a workspace

Running `rx init` a second time in a directory will shut down the current
remote machine and start a new one from scratch. This is essentially a wipe
back to the base state for your machine.
