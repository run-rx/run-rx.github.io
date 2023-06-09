---
layout: page
title: Python
permalink: /docs/python/
parent: Documentation
nav_order: 5
---

# Python language support

rx provides built-in support for Python projects. If you use a
[Python image](https://hub.docker.com/_/python), rx will set up a virtual
environment on your worker based on your _requirements.txt_ file. The virtual
environment is in _/venv_ on the remote machine and is activated prior to rx
running any commands.

Whenever your _requirements.txt_ file changes, rx will automatically download
new packages into your virtual environment. These packages will be built for
the worker's architecture (e.g., Cuda) and can often be installed pre-built
for popular packages/architectures, speeding up setup times.

See the [getting started](https://github.com/run-rx/getting-started/blob/master/03-requirements.py)
example for more info on _requirements.txt_.

Python environments have the environment variable `VIRTUAL_ENV` set and
prefix the `PATH` with _/root/venv_.
