---
layout: page
title: Output
permalink: /docs/output/
parent: Documentation
nav_order: 6
---

# Handling output files

When a command completes, rx copies all of the outputs created in your rx root
to rx-out on your local machine. For example, suppose you create two output
files:

    $ rx touch file1 rx-out/file2
    Created outputs:
      rx-out/file1
      rx-out/file2

Note that file1 is "swept" to _rx-out_, as it is created by the command.
_rx-out_ is a good place for intermediate outputs, as everything else on the
remote rxroot is wiped between commands to exactly match your local rxroot. For
example, if we now run `ls` on our remote rxroot, we can see that _file1_ has
disappeared:

    $ rx ls
    rx-out

...because it does not exist locally. However, it still exists in _rx-out_:

    $ rx ls rx-out
    file1 file2

rx makes a best-effort attempt to put the correct output in _rx-out_, but it
will often work better to write outputs there specifically. The example above
raises the question: what happens if there are conflicts? What if we try to
write file1 and rx-out/file1?

rx's logic is: probably the user wants everything under rxroot. However, if
they have also written a file with that name to _rx-out_, that's probably the
one they intend as output. However, if there's a more recently-created one
than the one in _rx-out_, that's probably the one they want.

That is, the precedence order is:

1. File with the latest modified timestamp.
2. File written to rx-out.
3. File written anywhere under rxroot.

This is somewhat complex to reason about so a good rule-of-thumb is: write
any outputs you want to _rx-out_.
