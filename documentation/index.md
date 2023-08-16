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

* The flag parsing library is very "grabby" and doesn't like flags it doesn't
  recognize. Thus, to run a command like `rx ls -l`, you must prevent rx from
  trying to parse `-l` (not a valid rx flag) by either wrapping the command in
  `'`s (`rx 'ls -l`') or indicate that rx should stop parsing parameters with
  `--`: `rx -- ls -l`.
* All commands are executed under Bash.
