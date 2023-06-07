---
layout: page
title: Configuration
permalink: /config/
---

# Creating a remote worker

You can run `rx init` anytime to reset or change your remote machine. When run,
`rx init` creates several JSON config files in a `.rx` directory in your
rx root. In particular, it creates a _remotes_ directory that contains
a couple of built-in machine configurations:

    project-root/
      .rx/
        remotes/
          default -> python-cpu
          python-cpu
          python-gpu
        trex.run-rx.com/
          ...

You can add any additional configurations you want. By default, `rx init` will
start the machine specified by _default_ (which starts as _python-cpu_: a
Python instance with default hardware specs).

## Changing Docker image

Machines can be configured to use any public Docker image, as specified in
the `image.docker` field. For example, if you wanted a plain Ubuntu machine
you could create a file _/path/to/rxroot/my-rx-remotes/vanilla-ubuntu_:

    {
      "image": {
        "docker": "ubuntu:22.04"
      }
    }

Then run `rx init` using the `--remote` option:

    $ rx init --remote=my-rx-remotes/vanilla-ubuntu

(Note that this will not do any of the [Python "magic"](/python) setup, as the
Ubuntu image is not necessarily being used for a Python project.)

## Configuring hardware requirements

*Note: this is not yet implemented!*

rx gives you a lot of flexibility in terms of RAM, disk, CPU, and GPU options
on your remote machine. (Or, at least, it will!) The files in _.rx/remotes_ are
starter templates and you can create any configuration you want.

To specify specific hardware requirements, set the `hardware` field in your
remote config:

    {
      "image": {
        "docker": "ubuntu:22.04"
      },
      "hardware": {
        "ram": "32GB",
        "disk": "64GB",
        "processor": "gpu",
      }
    }

When you specify custom hardware, rx will calculate how much those resources
will cost and ask you to confirm or set up payment before allocating the
machine. Depending on what you request, it may take rx a few minutes to
provision a suitable machine.
