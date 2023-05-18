---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

rx is a command-line tool to help make remote execution easy. Imagine a cloud
instance that is already set up, where packages are already installed, your
code is already available, and output is automatically synced back to your
local device.

## Installation

Install via pip:

    pip install run-rx

rx also requires rsync to run, make sure you have it installed:

    which rsync

If not, check out [its website](https://rsync.samba.org/download.html) or your
favorite package manager to install.

## Usage

In the directory containing your project (often your git root), run:

    rx init

This will prompt you to log in (or create an account) and allocate a machine
in the cloud for you to use. Then it will copy your project from your local
machine to the cloud instance and install any packages that your project needs.

It may take several minutes to allocate a machine, copy your source code, and install packages (depending on your project).

Once rx finishes initializing, you can run any command on your remote worker
by prefixing it with "rx":

    rx python my-script.py
    rx ps ax
    rx 'echo $PATH > my-path.txt'

Feel free to [file an issue](https://github.com/run-rx/rx/issues) if you have
any questions or problems!

# Current limitations

* stdin is not yet supported. This means that, if a command prompts for input,
  it'll just hang until you kill it. In particular, remember to pass `-y` to
  stuff like `pip install -y ...` or `apt-get install -y ...`.
* The flag parsing library is very "grabby" and doesn't like flags it doesn't
  recognize. Thus, to run a command like `rx ls -l`, you must prevent rx from
  trying to parse `-l` (not a valid rx flag) by either wrapping the command in
  `'`s (`rx 'ls -l`') or indicate that rx should stop parsing parameters with
  `--`: `rx -- ls -l`.
* You can only execute commands from your rx root at the moment, not a
  subdirectory of your project. If you need to execute a command from a
  subdirectory, prefix it with `cd my-subdir;`, e.g.,
  `rx 'cd path/to/dir; ls'`. Note the `'`s to prevent Bash from grabbing the
  `;`.
* All commands are executed under Bash.
