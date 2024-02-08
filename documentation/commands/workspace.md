---
layout: page
title: ws
permalink: /docs/commands/ws
parent: Subcommands
grand_parent: Documentation
nav_order: 2
---

# ws

Gets info about your current workspace. This supports several subcommands.

## commit

Stores the current state of the workspace for future use. By default the image
will be private to you. See the set-acls command for sharing this imge.

rx uses the directory name of your rxroot as the image name. For example, if
your username is `notch` and your project is in _~/gitroot/my-project_, rx will
store it as `notch/my-project`.

If you'd like to customize this you can specify the `--name` option:

    rx ws commit --name=minecraft

This will store the image is `notch/minecraft`. If you belong to an
organization, you can also store it under the org's namespace:

    rx ws commit --organization=msft --name=minecraft
    Storing your workspace...
    Your remote machine's state has been saved.

    If you'd like to initialize a new workspace with this state, use the following lines in your config:

    image:
      registry: registry.run-rx.com
      repository: notch/minecraft
      tag: '20240125'

See the [config docs](/docs/config) for more info about configuring images.

## info

This returns a yaml config of the workspace for this rx root, plus all commands
you've run this month.

## set-acls

By default workspaces are private to you: no one else has read or write
permissions.

If you'd like to create a publicly readable workspace (e.g., as a config for an
open source project), you can set that with the `--set-visibility` option:

    rx ws set-acls --set-visibility=public

You can make it private again with `--set-visibility=private`.

If you'd like to share it with individual users, you can do so with the `--add-reader` option:

    rx ws set-acls --add-reader=concernedape

You can also share the workspace with an organization that you're a member of:

    rx ws set-acls --add-reader=msft

See the [config docs](/docs/config) for more info about setting ACLs.
