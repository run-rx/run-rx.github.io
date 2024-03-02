---
layout: page
title: Remote configuration
permalink: /getting-started/python/remote-config
parent: Python
grand_parent: Getting Started
nav_order: 3
---

# Configuring your remote machine

rx gives you a lot of flexibility in terms of configuring your remote machine.
You can install any tools or dependencies you need, then store the state and
share it with anyone you want.

For example, suppose our program has a critical dependency on the `fortune`
binary. If we try running `fortune` on the remote machine, we can see that it's
not installed by default:

    $ rx fortune
    /bin/bash: line 1: fortune: command not found

We can install it from the package manager with:

    $ # The stripped-down container we start with starts with and empty package
    $ # index, so start by filling it in.
    $ rx apt-get update
    $ rx apt-get install fortune

Now we can run `fortune`. However, it's installed to /usr/games, which isn't on
the PATH, so we have to fully-specify its path:

    $ rx /usr/games/fortune
    Familiarity breeds contempt -- and children.
      		          -- Mark Twain

That's great, but we don't want to have to install it every time we init a
workspace! To commit the current state of our workspace, run:

    $ rx ws commit
    Storing your workspace...
    Pushed layer cb9317ff7c32: : 23501824 bytes [00:00, 32461083.90 bytes/s]
    Your remote machine's state has been saved.

    If you'd like to initialize a new workspace with this state, use the following lines in your config:

    image:
      registry: registry.run-rx.com
      repository: your-username/getting-started
      tag: '20240120'

Using the info above, create a new rx config, _my-rx-config.yaml_, in your
project directory:

    image:
      registry: registry.run-rx.com
      # Replace these lines with whatever your commit output actually printed.
      # ---
      repository: your-username/getting-started
      tag: '20240120'
      # ---
      environment_variables:
        PATH: /usr/games

This is the config from above, plus we add /usr/games to the PATH. (You can set
any environment variable you want in this section. Note that PATH is
special-cased to add it to the existing PATH.)

Let's try creating a new workspace using this as a template. Run:

    $ rx init --remote=my-rx-config.yaml

Now `fortune` should be installed and on the PATH:

    $ rx fortune
    Today is the first day of the rest of your life.

By default, any workspace images you create are private to your account. If
you'd like to share one with someone else, you can give them permission to use
it with the `set-acls` command:

    $ rx ws set-acls --add-reader=alice  # <-- Their rx username

They cannot change your stored image, but they can save a new version of it to
their account.

*For enterprise users*, you can easily give access to everyone at your
organization:

    $ rx ws set-acls --add-reader=wayne-tech.com

For open source projects, you may want to let anyone use the image:

    $ rx ws set-acls --set-visibility=public

This will allow anyone to read your workspace. If you change your mind and want
to make it private again, run:

    $ rx ws set-acls --set-visibility=private

See more info about permissions in [the docs](/docs/config). You can also
read more about storing and retreiving workspaces.

This concludes the getting started guide! You can now create a remote workspace,
use it to develop locally or remotely, and save and share it with others.

For more info, check out the [docs](/docs). If you have any questions, please
[let us know](https://github.com/run-rx/rx/issues).
