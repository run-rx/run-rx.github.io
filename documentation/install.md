---
layout: page
title: Installation
permalink: /docs/install/
parent: Documentation
nav_order: 1
---

# Installing rx

The easiest way to install rx is from pip:

    $ pip install run-rx

rx also requires rsync to run, make sure you have it installed:

    $ which rsync

If not, check out [its website](https://rsync.samba.org/download.html) or your
favorite package manager to install.

## Upgrading rx

The rx server checks the client version on every command. If a more recent
version of the client is required, rx will print an error message asking you
to upgrade, e.g.:

    Version 0.0.7 required (got 0.0.4)

    Upgrade to the latest version with `pip install --upgrade run-rx`

You can upgrade anytime with:

    pip install --upgrade run-rx

# rx source code

## Running from source

You can also check out the source code for rx on
[GitHub](https://github.com/run-rx/rx). You will need to install dependencies
and then generate the protobufs with:

    $ pip install requirements_dev.txt
    $ python -m grpc_tools.protoc -I. \
      --python_out=. --pyi_out=. --grpc_python_out=. \
      rx/proto/rx.proto

Then use:

    $ python -m rx <standard rx arguments and/or flags>

## Running tests

To run tests, install the dev requirements and then use the proided script:

    $ pip install -r requirements_dev.txt
    $ python run_tests.py
