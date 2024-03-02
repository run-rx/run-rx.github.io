---
layout: page
title: Output files
permalink: /getting-started/python/output
parent: Python
grand_parent: Getting Started
nav_order: 1
---

# Accessing outputs created remotely

You may want access to artifacts that your program produces: binaries, images,
models, etc. As long as they are created under the rx root directory (the
directory where you ran "rx init"), then they will be automatically synced back
to your client.

For example, try redirecting output to a file:

    $ rx 'date > my-date'
    Changed:
      my-date

Note the quotes around the command: if you do not quote it, your local shell
will grab the redirect before it can be sent to the remote machine!

Now run `ls` and you can see that rx copied the output back to your local
directory:

    $ ls
    hello-world.py    my-date

Check out the documentation on [outputs](/docs/output) for more info.

Next, we'll try
[adding some dependencies](/getting-started/python/requirements)!
