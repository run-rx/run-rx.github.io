---
layout: page
title: Documentation
permalink: /docs/
has_children: true
nav_order: 3
---

# Documentation

rx is a command-line tool that makes it easy to run code remotely.

To get started, check out [installation](/docs/install) or
[getting started](/getting-started) sections.

## Feedback

Feel free to [file an issue](https://github.com/run-rx/rx/issues) if you have
any questions or problems!

## Current limitations

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
