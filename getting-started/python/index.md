---
layout: page
title: Python
permalink: /getting-started/python
parent: Getting Started
has_children: true
nav_order: 3
---

# Getting started guide for Python

Welcome to rx! If you haven't already, create a directory you'd like to use and
add a Python file with the following content:

    import socket

    def main():
      print(f'Hello world, I am {socket.gethostname()}')

    if __name__ == '__main__':
      main()

This gets the hostname of the machine it's running on. Try running this script
"normally":

    $ python hello-world.py
    Hello world, I am ks-macbook-air.lan

This should print the name of your current local machine. Now create a remote
machine that mirrors your local state by running `rx init`:

    $ rx init

This sets up rx in the current directory, similar to "git init". It will
prompt you to log in and/or create an rx account. Then it will set up a
machine for you in the cloud and copy over any local files (just
_hello-world.py_ at the moment).

Now run your script in the cloud by adding "rx" before the python command:

    $ rx python hello-world.py
    Hello world, I am getting-started.rx

Congratulations, you just ran a Python script remotely! Try changing this
script to print "Goodbye from &lt;hostname&gt;" and run
`rx python hello-world.py` again:

    $ rx python hello-world.py
    Goodbye from getting-started.rx!

As you can see, the changes you made locally are immediately available on your
remote instance. You can run any other commands you want on your instance, just
prefix them with "rx":

    $ rx pwd
    $ rx 'ls -lh > ls-out'
    $ rx which python

Feel free to continue to experiment with this script or check out the next
section on [output](/getting-started/python/output).
