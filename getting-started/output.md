---
layout: page
title: Output files
permalink: /getting-started/output
parent: Getting Started
nav_order: 2
---

# Accessing outputs created remotely

You may want access to artifacts that your program produces: binaries, images,
models, etc. As long as they are created under the rx root directory (the
directory where you ran "rx init"), then they will be automatically synced back
to your client.

For example, try redirecting output to a file:

    $ rx 'date > my-date'
    Created outputs:
      my-date

Note the quotes around the command: if you do not quote it, your local shell
will grab the redirect before it can be sent to the remote machine!

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

This writes the current time to _timestamps/now.txt_. Try running this script on
rx:

    $ rx python output.py
    Wrote timestamps/now.txt
    Created outputs:
      timestamps/now.txt

You can see that rx copied the output back to your local directory. Check out
the documentation on [outputs](/docs/output) for more info.

Next, [requirements](/getting-started/requirements)!
