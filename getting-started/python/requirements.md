---
layout: page
title: Python dependencies
permalink: /getting-started/python/requirements
parent: Python
grand_parent: Getting Started
nav_order: 2
---

# Installing Python dependencies

rx attempts to automatically set up a virtual environment for your scripts
and install any packages that they need.

Try this out by creating a Python file that depends on an uninstalled package,
`art`:

```
import sys

import art

def main():
  if len(sys.argv) < 2:
    print('You must pass in a string to print.')
    return
  art.tprint(' '.join(sys.argv[1:]))

if __name__ == '__main__':
  main()
```

Try running this script with rx:

    $ rx python reqs.py 'more cowbell'

This will print a `ModuleNotFoundError`, because `art` isn't found.

To install the `art` package remotely, create a _requirements.txt_ file
(locally) and add a line:

    art==5.8

Then save _requirements.txt_ and go back to the command line. Try running this
script again and now rx has all of the packages it needs:

    $ rx python reqs.py 'more cowbell'
                                                           _            _  _
     _ __ ___    ___   _ __   ___    ___   ___  __      __| |__    ___ | || |
    | '_ ` _ \  / _ \ | '__| / _ \  / __| / _ \ \ \ /\ / /| '_ \  / _ \| || |
    | | | | | || (_) || |   |  __/ | (__ | (_) | \ V  V / | |_) ||  __/| || |
    |_| |_| |_| \___/ |_|    \___|  \___| \___/   \_/\_/  |_.__/  \___||_||_|

Note that you did not even need to install the package locally: rx took care of
installing packages based on the contents of requirements.txt.

Next section: configuring your
[remote machine](/getting-started/python/remote-config).
