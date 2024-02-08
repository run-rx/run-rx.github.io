---
layout: page
title: Documentation
permalink: /docs/
has_children: true
nav_order: 3
---

# Documentation

rx is a command-line tool that makes it easy to set up, use, and share a remote
environment while letting you continue to use all of your favorite local tools.

To get started, check out [installation](/docs/install) or
[getting started](/getting-started) sections.

## Feedback

Feel free to [file an issue](https://github.com/run-rx/rx/issues) if you have
any questions or problems!

## Current limitations

* All commands are executed under Bash.
* Bash will grab shell redirects, pipes, and so on before they can be passed to
  rx. Basically, if you're using a non-alphanumeric character, it will probably
  work better if you wrap the line in single quotes, e.g.: `rx 'cat f | head'`.
