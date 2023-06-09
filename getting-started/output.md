---
layout: page
title: Output files
permalink: /getting-started/output
parent: Getting Started
nav_order: 2
---

You may want access to artifacts that your program produces: binaries, images,
models, etc. As long as they are created under the rx root directory (the
directory where you ran "rx init"), then they will be automatically synced back
to your client.


For example, try redirecting output to a file under rx-out:

  $ rx 'date > rx-out/my-date'
  Created outputs:
    rx-out/my-date

Note the quotes around the command: if you do not quote it, your local shell
will grab the redirect before it can be sent to the remote machine!

If you run `ls` on the rx-out directory (locally or via rx), you can see it now
contains the output of your command.

rx-out is a special output directory that we encourage you to write files to.
However, rx will also make a best-effort attempt to "sweep" any other outputs
that were created into rx-out.

Create a file named _output.py_ containing the following Python script:

    import datetime
    import pathlib

    def main():
      output_dir = pathlib.Path('timestamps')
      output_dir.mkdir(parents=True, exist_ok=True)
      out_file = output_dir / 'now.txt'
      with out_file.open(mode='wt', encoding='utf-8') as fh:
        fh.write(
          f'At the sound of the beep, the time is: {datetime.datetime.now()}')
      print(f'Wrote {out_file}')

    if __name__ == '__main__':
      main()

This writes the current time to _timestamps/now.txt_. Try running this script on rx:

    $ rx python output.py
    Wrote timestamps/now.txt
    Created outputs:
      rx-out/timestamps/now.txt

You can see that rx copied the output back to your local directory.

Note that rx-out is a good place for intermediate outputs, as the rest of
the remote directory is reset to exactly mirror your local machine before each
command.

Next, [requirements](getting-started/requirements)!
