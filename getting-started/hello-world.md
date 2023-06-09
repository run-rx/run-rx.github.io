---
layout: page
title: Hello, world!
permalink: /getting-started/hello-world
parent: Getting Started
nav_order: 1
---

Welcome to rx! If you haven't already, create a directory you'd like to use
(or clone the [getting-started](https://github.com/run-rx/getting-started)
repository) and run `rx init`.

To start with, create a Python file with the following content:

    import socket

    def main():
      print(f'Hello world, I am {socket.gethostname()}')

    if __name__ == '__main__':
      main()

This gets the hostname of the machine it's running on. Try running this script
"normally":

    $ python hello-world.py
    Hello world, I am ks-macbook-air.lan

This should print the name of your current local machine. To run this in the
cloud, add "rx" before the python command:

    $ rx python hello-world.py
    Hello world, I am getting-started.rx

Congratulations, you just ran a python script remotely! Try changing this
script to print "Goodbye from <hostname>" and run "rx python hello-world.py"
again:

    $ rx python hello-world.py
    Goodbye from getting-started.rx!

As you can see, the changes you made locally are immediately available on your
remote instance. You can run any other commands you want on your instance, just
prefix them with "rx":

    $ rx pwd
    $ rx 'ls -lh > ls-out'
    $ rx which python

Feel free to continue to experiment with this script or check out the next
section on [output](/getting-started/output).
