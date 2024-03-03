---
layout: page
title: Running a "local" server
permalink: /getting-started/node/devserver
parent: Node.js
grand_parent: Getting Started
nav_order: 2
---

# Running a "local" server

rx lets you forward remote ports to your local machine. This has higher latency
than truly running a server locally, but can be handy for sharing work with
coworkers or using several development devices.

To get started, we'll create a simple Express server:

```
// my_server.js
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello World');
})

console.log('Listening on localhost:3000...');
app.listen(3000);
```

Create/add the `express` package as a dependency in package.json:

    {
      "name": "hello-rx",
      "dependencies": {
        "express": "^4.18.3"
      }
    }

Now we have to tell rx that we're going to be using port 3000. `rx` autodetects
a lot of info about your setup, but unfortunately it cannot figure out what
ports you want to use! (Yet.)

Create a file, _my-express.yaml_:

    image:
      ports:
        - 3000

Now tell rx to use this configuration by running:

    $ rx init --remote=my-express.yaml

This will recreate your remote machine, open up port 3000, and map it to your
local port 3000. However, there's nothing running on 3000 yet! To start the
server, run:

    $ rx node my_server.js

Now visit [localhost:3000](http://localhost:3000) in your browser and it will
show "Hello World".

# Next steps

This concludes the getting started guide! You can now create a remote workspace,
use it to develop locally or remotely, and serve your work locally.

For more info, check out the [docs](/docs). If you have any questions, please
[let us know](https://github.com/run-rx/rx/issues).
