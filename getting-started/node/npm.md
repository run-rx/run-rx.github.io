---
layout: page
title: Dependency management
permalink: /getting-started/node/npm
parent: Node.js
grand_parent: Getting Started
nav_order: 1
---

# Managing _node\_modules_

rx attempts to automatically install any dependencies your project needs.

Try this out by creating a Javascript file that depends on an uninstalled
package, `cowsay`:

```
const cowsay = require('cowsay');

console.log(cowsay.say({text : 'Moooore cowbell'}));
```

Try running this script with rx:

    $ rx node cow_stuff.js

This will print an error like: `Error: Cannot find module 'cowsay'`.

To install the `cowsay` package remotely, create a _package.json_ file
(locally), either by running `npm init; npm install cowsay` or just
copy-pasting:

    {
      "name": "hello-rx",
      "dependencies": {
        "cowsay": "^1.6.0"
      }
    }

Then save _package.json_ and go back to the command line. Try running this
script again and rx will detect that package.json has a new dependency and take
care of installing it before running your script:

    $ rx node cow_stuff.js
    _________________
    < Moooore cowbell >
    -----------------
            \   ^__^
            \  (oo)\_______
                (__)\       )\/\
                    ||----w |
                    ||     ||

Note that you did not even need to install the package locally: rx took care of
installing packages based on the contents of _package.json_.

# Syncing _node\_modules_ directly

By default, `rx` creates a clean `node_modules` install from your package.json
(or package-lock.json) file. In general, this works better than using your
existing _node\_modules_ since weird _node\_modules_ state is a frequent source
of bugs.

However, if you'd like for `rx` to use your local version, you can remove the
`node_modules` line from `.rxignore` (automatically created when you run
`rx init`).

# Next steps

Usually Node is used for web programming, not terminal tooling! Check out the
next section to start
[running a devserver](/getting-started/node/devserver).
