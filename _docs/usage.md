---
layout: documentation
title: Usage
description: Available commands and options of thelounge, the CLI of The Lounge
order: 3
---

Once The Lounge is installed, a program called `thelounge` is now available.

{% include toc.md %}

## Command line help

To get general information about the program and an overview of the available
commands, use the `--help` (or `-h`) option:

```
thelounge --help
```

To get specific help for a given command, run:

```
thelounge <command> --help
```

For example, to know how to use `thelounge start` and the options available,
run:

```
thelounge start --help
```

If you need to check which version of The Lounge is installed, use:

```
thelounge version
```

## Using the correct system user

Note that all commands **must** be executed as the same user The Lounge will be run as.

### Unix like systems:
If you installed The Lounge via the package manager of your distro and plan to run it as a system service, the user is called "thelounge". So every command needs to be executed as `sudo -u thelounge thelounge <command>`, where `<command>` should be substituted with a subcommand like `start` or `add`

## Starting the server

To start the server, run the following command:

```
thelounge start
```

This will start a server and display something along the lines of:

<div class="terminal">
  <span class="terminal-log-info"></span>
  Configuration file created at <span class="terminal-green">/etc/thelounge/config.js</span>.<br>

  <span class="terminal-log-info"></span>
  The Lounge <span class="terminal-green">v3.0.0</span> (Node.js <span class="terminal-green">8.9.2</span> on <span class="terminal-green">linux</span> x64)<br>

  <span class="terminal-log-info"></span>
  Configuration file: <span class="terminal-green">/etc/thelounge/config.js</span><br>

  <span class="terminal-log-info"></span>
  Available at <span class="terminal-green">http://:::9000/</span> in <strong style="color: white">private</strong> mode<br>

  <span class="terminal-log-info"></span>
  There are currently no users. Create one with <strong style="color: white">thelounge add &lt;name&gt;</strong>.
</div>

This tells us a few things:

- Since it is the first time The Lounge runs, a configuration file was created.
  Its location depends on how The Lounge was installed (see
  [the installation page](/docs/install-and-upgrade)).
- The Lounge can now be accessed at <http://localhost:9000/>.
- It has started in **private** mode, which means only users who
  have an account can log in. There is no guest access.
- There are no user accounts as of yet, so in fact, no one can log in for now
  (see the [user management](/docs/users) page).

The process can be stopped at any time by hitting <kbd>Ctrl</kbd>+<kbd>C</kbd>.
This will effectively close all connections to remote IRC servers that users are
connected to.

## Specifying a different configuration file

It can be useful to provide a different location for the configuration file. For
example, you might want to store it on another partition, or you might want to
run multiple instances with different configurations.

To do so, use the environment variable called `THELOUNGE_HOME`. It will instruct
a location where The Lounge will look for the configuration file, the available
users, etc.

For example, to start a server with a configuration located at `/tmp/config.js`,
run:

```
THELOUNGE_HOME=/tmp thelounge start
```

## Installing additional themes

A list of all available themes can be found [on the npm registry](https://www.npmjs.com/search?q=keywords%3Athelounge-theme) and installed with `thelounge install`. For example, to install a theme called `thelounge-theme-solarized`, run:

```
thelounge install thelounge-theme-solarized
```

After restarting The Lounge, the theme will now be available in the client settings.

Additionally, any theme can be used as the default one for all clients. See [the `theme` section on the configuration page](/docs/configuration#theme) for more information.

## Configuring The Lounge

As shown above, The Lounge starts by default in **private** mode on port
**9000**.

To change the mode or port quickly, the `--config` (or `-c`) option can be used.

For example, to start The Lounge on port **9001**, run:

```
thelounge start --config port=9001
```

Similarly, to start it in **public** mode, run:

```
thelounge start --config public=true
```

This option can be specified multiple times to match the requested
configuration:

```
thelounge start -c port=9001 -c public=true
```

However, `--config` is not limited to setting the port or mode. In fact, any
option available in the configuration file can be passed using `--config`.
See the [configuration page](/docs/configuration) for a full list.

A few rules apply to the `--config` option:

- Nested objects require using a dot-notation. For example:
  ```
  thelounge start -c debug.raw=true
  ```
- Lists of values must be wrapped with `[]`. For example:
  ```
  thelounge start -c transports=[websocket,polling]
  ```
- If a value has a whitespace, it must be wrapped in quotes. For example:
  ```
  thelounge start -c defaults.name="Cool Network"
  ```
