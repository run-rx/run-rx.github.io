---
layout: page
title: Configuration
permalink: /docs/config/
parent: Documentation
nav_order: 3
---

# Creating a remote worker

You can run `rx init` anytime to reset or change your remote machine. When run,
`rx init` creates several JSON config files in a `.rx` directory in your
rx root. In particular, it creates a _remotes_ directory that contains
a couple of built-in machine configurations:

    project-root/
      .rx/
        remotes/
          default -> python-cpu.json
          python-cpu.json
          python-gpu.json
        trex.run-rx.com/
          ...

You can add any additional configurations you want. By default, `rx init` will
start the machine specified by _default_ (which starts as _python-cpu.json_: a
Python instance with default hardware specs).

## Changing Docker image

Machines can be configured to use any public Docker image, as specified in
the `image.docker` field. For example, if you wanted a plain Ubuntu machine
you could create a file _/path/to/rxroot/my-rx-remotes/vanilla-ubuntu.json_:

    {
      "image": {
        "docker": "ubuntu:22.04"
      }
    }

Then run `rx init` using the `--remote` option:

    $ rx init --remote=my-rx-remotes/vanilla-ubuntu.json

(Note that this will not do any of the [Python "magic"](/python) setup, as the
Ubuntu image is not necessarily being used for a Python project.)

### Limitations

You can use any publicly-available Docker image. If you'd like to use a
private image, please [email us](mailto:eng@run-rx.com) and we can
set up secure access to your company's registry.

At the moment, there is a cap of 8GB on image size. Again, please
[email us](mailto:eng@run-rx.com) if you'd like to use a larger image.

### Pricing

Unlimited image usage and switching between images is included in the monthly
base price. See the [pricing page](https://www.run-rx.com/pricing) for more
details.

## Configuring hardware requirements

By default, rx provides a CPU-based machine. If you'd like to use a GPU, add
a the `"processor": "gpu"` field to your config. For example:

    {
      "image": {
        "docker": "python:3.10-slim"
      },
      "hardware": {
        "processor": "gpu",
      }
    }

Note the using a GPU is charged

If you need a specific type of GPU or more powerful/extensive hardware, please
[email us](mailto:eng@run-rx.com) and we can immediately provision it for you
(this will be handled automatically in the future, but is hand-provisioned at
the moment).

## Pricing

See the [pricing page](https://www.run-rx.com/pricing) for more details about
CPU and GPU pricing.
