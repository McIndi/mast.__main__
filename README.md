# MAST

__Note__: This repository is for tracking bugs in the MAST project as well as 
acting as a central hub for documentation.

MAST is a tool to automate administration and operations for groups of 
systems. From here on we will refer to `Environments`, which we will define
as arbitrary groups of systems. Currently, there is only MAST for IBM 
DataPower, but soon there will be (among others):

* MAST for Docker
* MAST for Splunk
* MAST for Windows
* MAST for Linux

MAST, as it exists now, is comprised of the following Python modules:

1. mast.cli
2. mast.config
3. mast.cron
4. mast.daemon
5. mast.hashes
6. mast.installer
7. mast.logging
8. mast.plugins
9. mast.plugin_utils
10. mast.pprint
11. mast.timestamp
12. mast.xor

Each of these is meant to ease some common issues related with systems
administration. I will attempt to give a brief defination of each.
Please note that more may be added in the future.

## mast.cli

mast.cli is a library designed to create command line interaces to
Python functions based on their function signatures. This library
provides a single class `Cli` which itself provides a few useful
functions two of which are: a decorator used to designate a function
as a `sub-command`, and a `Run` method which should be called from
within a `if __name__ == "__main__":` block.

__NOTE__: The mast.cli module uses `argparse` behind the scenes.

__NOTE__: Currently, some mast modules use the `commandr` library
for this same purpose, but as it uses `optparse` behind the scenes,
we decided to ship our own which uses the more modern `argparse` module.
As a result of this, either module is available for your use, but the commandr
library may cease to be shipped with MAST, but it can easily be installed using
the pip utility shipped with MAST.

More documentation as well as the source code can be found 
[in the repository](https://github.com/mcindi/mast.cli).

## mast.config

When MAST is installed the `prefix` is hard-coded into certain places
where mast libraries and utilities can have access to it. Based on this
`prefix`, we can rely on certain things. One of these things we can rely
on is the existance of the directories `$MAST_HOME/etc/default` and 
`MAST_HOME/etc/local`. The mast.config module provides some convenience
methods for merging configuration files stored in these directories.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.config).

## mast.cron

mast.cron is written as a plugin for mast.daemon, This plugin provides a 
cross-platform cron-style scheduler. Any tasks defined in 
`$MAST_HOME/etc/crontab` will be executed based on their definition while 
`mast.daemon` is running.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.cron).

## mast.daemon

__Note__: This is unfinished in the initial beta release, but should be
fixed very soon, I will remove this note when that is done

mast.daemon provides a cross-platform service which mast utilities can
"plug-in" to. mast.cron is an example of one such utility, and more are 
being planned for the future. By creating a Python package and defining an
`entry_point` of mast_daemon_plugin and pointing that `entry_point` at a
subclass of `threading.Thread` you can create a `mastd plugin`. a 
`mastd plugin` is simply a thread which is started by `mastd` and checked
every minute to see if it is alive. If it is not alive, it is restarted,
otherwise, nothing is done.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.daemon).


### installing mastd

There are different procedures for "installing mastd" depending on which platform
you are running on.

#### Windows

On Windows, a utility is provided (TODO: Where?) which uses Mark Hammond's `win32util`
library to install a Windows service which can then be started, stopped or restarted
in the normal way, or you can use the mastd utility to perform these same actions.

#### Linux

On Linux mastd can be started, stopped or restarted using the mastd utility.
In order to "install" this onto your system please follow your system's
init daemon's instructions for installing services. For convenience a sample
`init script` and a sample `systemd spec` is provided in the `$MAST_HOME/etc`
directory which can be used to install them on most Linux systems.

#### Mac OSx

Comming soon

### mast.hashes

mast.hashes is a Python module which provides some convenient helper functions to
compute some common hashes of a string or file.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.hashes).

### mast.installer

mast.installer is a utility to build the installers for various platforms. Please note
that mast.installer as it exists needs an existing Python installation to execute. If
you simply wish to install MAST it is recomended to use our pre-built executables
in order to install

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.installer).

### mast.logging

mast.logging provides some handy functions to assist in logging for mast utilities.
It provides one function and one decorator, which creates a logger and logs the execution
of a function (including arguments passed) respectively.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.logging).


### mast.plugins

mast.plugins provides some convenient base classes for implementing plugins for mast.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.plugins).

### mast.plugin_utils

mast.plugin_utils provides some convenient methods for creating web forms based on function
signature and for executing those functions on form submission.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.plugin_utils).


### mast.pprint

mast.pprint provides some functions for pretty_printing certain data structures.

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.pprint.)

### mast.timestamp

mast.timestamp provides a class called Timestamp. When this class is instanciated,
it captures the current date-time and the instance can be used to present this
date-time in various formats

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.timestamp).

### mast.xor

mast.xor provides two methods `xorencode` and `xordecode` which do exactly
what you would expect. A key parameter can be passed to set the
"key" or "password" for the xor operation. The key defaults to "\_".

More documentation as well as the source code can be found
[in the repository](https://github.com/mcindi/mast.xor).

## Installation

Comming soon


