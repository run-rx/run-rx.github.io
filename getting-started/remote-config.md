---
layout: page
title: Remote configuration
permalink: /getting-started/remote-config
parent: Getting Started
nav_order: 4
---

# Configuring your remote machine

rx gives you a lot of flexibility in terms of RAM, disk, CPU, and GPU options
on your remote machine. (Or, at least, it will!)

You can check out your current configuration by looking at
_.rx/remotes/default_. When you run `rx init`, rx uses that to provision a
bog-standard Python 3.11 instance.

However, the files in .rx/remotes are simply starter templates and you can
create any configuration you want.

For example, `removeprefix` is a string method added in Python 3.9. Try
creating a file that uses it:

    PY_PROJECTS = ['PyTorch', 'PyPi', 'PyMongo']
    print('Some Python projects:')
    for proj in PY_PROJECTS:
      print(proj.removeprefix('Py'))

Create a configuration that uses Python 3.7 by creating a file called
`my-py37` containing:

    {
      "image": {
        "docker": "python:3.7-slim"
      }
    }

Now tell rx that you want to use this configuration by running `rx init`
again, this time with the `--remote` flag:

    $ rx init --remote=py37

Now if you run this script, you should see:

    $ rx python 04-remote-config.py
    Some Python projects:
    Traceback (most recent call last):
      File "04-remote-config.py", line 44, in <module>
        print(proj.removesuffix('Py'))
    AttributeError: 'str' object has no attribute 'removesuffix'

To upgrade to Python 3.11, run `rx init` again without any flags and it'll
go back to using the config `default` is symlinked to. Now it prints:

    $ rx python 04-remote-config.py
    Some Python projects:
    Torch
    Pi
    Mongo

In the future these remote config files will be used to specify hardware
requirements, too.

Now you know the basics of how to use rx. Check out the other [docs](/docs) for
more details!
