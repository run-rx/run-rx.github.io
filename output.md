---
layout: page
title: Output
permalink: /output/
---

You may want access to artifacts that your program produces: binaries, images,
models, etc. As long as they are created under the rx root directory (the
directory where you ran `rx init`), then they will be automatically synced back
to your client.

For example, try redirecting output to a file under rx-out:

    $ rx 'date > rx-out/my-date'
    Created outputs:
      rx-out/my-date

_Note the quotes around the command: if you do not quote it, your local shell
will grab the redirect before it can be sent to the remote machine._

If you run `ls` on the rx-out directory (locally or via rx), you can see it now
contains the output of your command.

rx-out is a special output directory that we encourage you to write files to.
However, rx will also make a best-effort attempt to "sweep" any other outputs
that were created into rx-out.

For example, try running this script on rx:

    $ rx 'date > another-date'
    Wrote timestamps/now.txt
    Created outputs:
      rx-out/timestamps/now.txt

Note that rx-out is a good place for intermediate outputs, as the rest of
the remote directory is reset to exactly mirror your local machine before each
command.
