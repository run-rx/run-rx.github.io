---
layout: page
title: Python
permalink: /docs/python/
parent: Documentation
nav_order: 5
---

# Python language support

rx provides built-in support for Python projects that use pip and/or conda for
dependency management. If you have a requirements.txt or environment.yml file,
rx will automatically set up an environment on your worker based on that file.

## Pip

To automatically keep a pip environment up-to-date, the Docker image you chose
must have Python interpreter installed (version 3.7+). Consider using one of
the [Python images](https://hub.docker.com/_/python). By deafult, the virtual
environment is in _/root/venv_ on your worker and is activated prior to rx
running any commands.

Whenever your _requirements.txt_ file changes, rx will automatically download
new packages into your virtual environment. These packages will be built for
the worker's architecture (e.g., Cuda) and can often be installed pre-built
for popular packages/architectures, speeding up setup times.

See the
[getting started](https://github.com/run-rx/getting-started/blob/master/03-requirements.py)
example for more info on _requirements.txt_.

Pip environments have the environment variable `VIRTUAL_ENV` set and
prefix the `PATH` with _/root/venv_.

## Conda

To automatically keep a Conda environment up-to-date, the Docker image you
choose must have Conda installed. Consider using the rx's own Conda-optimized
container by specifying in your [config](/docs/config):

    {
      "image": {
        "repository": "runrx/conda",
      },
      "hardware": {
        "processor": "gpu",
      }
    }
