---
layout: page
title: 'Node.js'
permalink: /getting-started/node
parent: Getting Started
has_children: true
nav_order: 2
---

# Getting started guide for Node.js

Welcome to rx! If you haven't already, create a directory you'd like to use for
this guide.

To get started, create a _hello\_world.js_ file with the following content:

    const os = require('os');
    console.log(`Hello world, I am ${os.hostname()}`);

This gets the hostname of the machine it's running on. Try running this script
with `node` directly:

    $ node hello_world.js
    Hello world, I am ks-macbook-air.lan

This should print the name of your current local machine. Now create a remote
machine that mirrors your local state by running `rx init`:

    $ rx init

This sets up rx in the current directory, similar to "git init". It will
prompt you to log in or create an rx account. Then it will set up a
machine for you in the cloud, detect that your project is using Node, set that
up, and copy over any local files (just _hello\_world.js_, at the moment).

Now run your script in the cloud by adding "rx" before the `node` command:

    $ rx node hello_world.js
    Hello world, I am getting-started.rx

Congratulations, you just ran a Node script remotely! Try changing this
script to print "Goodbye from &lt;hostname&gt;" and run
`rx node hello_world.py` again:

    $ rx node hello_world.js
    Goodbye from getting-started.rx!

As you can see, the changes you made locally are immediately available on your
remote instance. You can run any other commands you want on your instance, just
prefix them with "rx":

    $ rx pwd
    $ rx 'ls -lh > ls-out'
    $ rx which npm

Feel free to continue to experiment with this script or check out the next
section on [managing dependencies](/getting-started/node/npm).
