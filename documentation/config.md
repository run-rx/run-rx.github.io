---
layout: page
title: Configuration
permalink: /docs/config/
parent: Documentation
nav_order: 3
---

# Creating a remote worker

You can run `rx init` anytime to reset or change your remote machine. When run,
`rx init` creates several YAML config files in a `.rx` directory in your
rx root. In particular, it creates a _remotes_ directory that contains
a couple of built-in machine configurations:

    project-root/
      .rx/
        remotes/
          default -> python-cpu.yaml
          python-cpu.yaml
          python-gpu.yaml
        trex.run-rx.com/
          ...

You can add any additional configurations you want. By default, `rx init` will
start the machine specified by _default_ (which starts as _python-cpu.yaml_: a
Python instance with default hardware specs).

## Changing Docker image

Machines can be configured to use any public Docker image, as specified in
the `image.docker` field. For example, if you wanted a plain Ubuntu machine
you could create a file _/path/to/rxroot/my-rx-remotes/vanilla-ubuntu.yaml_:

    image:
      repository: "ubuntu:22.04"

Then run `rx init` using the `--remote` option:

    $ rx init --remote=my-rx-remotes/vanilla-ubuntu.yaml

### Limitations

You can use any publicly-available Docker image. If you'd like to use a
private image, please [let us know](https://github.com/run-rx/rx/issues).

At the moment, there is a cap of 8GB on image size. Again, please
[email us](mailto:eng@run-rx.com) if you'd like to use a larger image.

### Pricing

Unlimited image usage and switching between images is included in the monthly
base price. See the [pricing page](https://www.run-rx.com/pricing) for more
details.

## Configuring hardware requirements

By default, rx provides a CPU-based machine. If you'd like to use a GPU, add
a the `processor: "gpu"` field to your config. For example:

    image:
      repository: "python:3.10-slim"
    remote:
      hardware:
        processor: "gpu"

Note the using a GPU machine incurs an hourly metered charge.

If you need a specific type of GPU or more powerful/extensive hardware, please
[file an issue](https://github.com/run-rx/rx/issues) or [email
us](mailto:eng@run-rx.com).

## Pricing

See the [pricing page](https://www.run-rx.com/pricing) for more details about
CPU and GPU pricing.
