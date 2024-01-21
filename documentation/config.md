---
layout: page
title: Configuration
permalink: /docs/config/
parent: Documentation
nav_order: 3
---

# Configuring a Remote Workspace

When you run `rx init`, rx sets up what we call a "workspace," which is a
Docker container on a remote host. You have a lot of control over how this
container is set up and configured. This documentation covers using and
configuring workspaces.

## The Config File

rx determines the type of container and hardware to use remotely based on the
contents of a YAML file. If you do not specify a path to a YAML file, rx
defaults to using the one _.rx/remotes/default_ is symlinked to. By default,
this is symlinked to _.rx/remotes/python-cpu.yaml_, a container on a standard
remote machine with a recent version of Python installed.

To modify this behavior, you can use a different config file, either by changing
the target the _default_ symlink points to or by specifying a path on the
command line:

    $ rx init --remote=some/path/to/my/config.yaml

Once a workspace is initialized the config file is not re-read.

A config file has two sections:

* `image`: describes the Docker container to start.
  * `registry`: Optional, defaults to Docker Hub.
  * `repository`: The Docker image name.
  * `tag`: Defaults to latest.
  * `envrionment_variables`: Key/value pairs of environment variables to set
    for the workspace.
* `remote`: describes the machine the workspace should be put on.
  * `hardware`: The CPU, memory, and disk requirements.
    * `processor`: The type of processor needed.

### Using an Existing Config

If a project has an existing rx config then you can use it to quickly initialize
a workspace. For example, suppose you have cloned an open source project
with an rx.yaml file. You can run:

    $ rx init --remote=rx.yaml

This will set up a workspace in the cloud with the config specified in the
`rx.yaml` file.

### Modifying a Workspace

As you work on a project you may install tools, edit configs, or generate
artifacts on the remote machine. If you'd like to save that state, you can run:

    $ rx ws commit
    Storing your workspace...
    Pushed layer cb9317ff7c32: : 23501824 bytes [00:00, 32461083.90 bytes/s]
    Your remote machine's state has been saved.

    If you'd like to initialize a new workspace with this state, use the following lines in your config:

    image:
      registry: registry.run-rx.com
      repository: username/rx-root-dir
      tag: '20240120'

This will save the current state of your workspace. (Note that this is not
useful for saving the current state of your project, since that is synced from
your local device every time you run a command.)

The output of the `commit` command prints the stanza you'd need to put in your
config to init a remote workspace from this shapshot. You can also always get
this infomation by running `rx ws info`.

### Sharing Configs

By default, your user is the only one who access to the workspace images you
create. However, you may want to share your image with others. Sharing your
image allows others to start up their own workspace with the given state, but
does not allow them to write new versions of it to your repository. They can,
however, write their own version to their own repository.

To share your image with a user (in this case, "trexbot"), run:

    $ rx ws set-acls --add-reader=trexbot

If you are using rx with an enterprise plan you can also share images with
groups that you are a member of:

    $ rx ws set-acls --add-reader=wayne-tech.com
    $ # or a subgroup:
    $ rx ws set-acls --add-reader=qa.wayne-tech.com

You must be a member of a group to share it with them.

For open source projects, you may want to give anyone access to use a
pre-configured environment. You can do this by setting the default visibility
to public:

    $ rx ws set-acls --visibility=public

If you change your mind you can set the visibility back to "private" (the
default).

## Default Configs

When first run, `rx init` creates several YAML config files in a `.rx` directory
in your rx root. In particular, it creates a _remotes_ directory that contains
a couple of built-in configurations:

    project-root/
      .rx/
        remotes/
          default -> python-cpu.yaml
          python-cpu.yaml
          python-gpu.yaml
        trex.run-rx.com/
          ...

You can add any additional configurations you want.

## Changing the Docker Image

Machines can be configured to use any public Docker image, as specified in
the `image.repository` field. For example, if you wanted a plain Ubuntu machine
you could create a file _/path/to/rxroot/my-rx-remotes/vanilla-ubuntu.yaml_:

    image:
      repository: ubuntu
      tag: "22.04"

Then run `rx init` using the `--remote` option:

    $ rx init --remote=my-rx-remotes/vanilla-ubuntu.yaml

### Limitations

You can use any publicly-available Docker image. If you'd like to use a
private image, please [let us know](https://github.com/run-rx/rx/issues).

At the moment, there is a cap of 8GB on image size. Again, please
[email us](mailto:eng@run-rx.com) if you'd like to use a larger image.
