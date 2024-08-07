# Modules

Modules are individual bash scripts containing code and functions that complete specific tasks.

> Modules may sometimes be referred to as function files or just functions are located in the functions directory and not be confused with bash functions. Modules have been named as such to avoid confusion.

A command will call upon modules to complete various command tasks. Modules are normally created if a task needs to be called upon by multiple commands, or as a logical way to split large commands and modules into smaller sub-modules.

Modules are located in the `modules` directory,

```text
lgsm/modules
```

## Module Groups

Modules are split into logical groups depending on the type of task being carried out.

-   **alert** - Sending alert notifications
-   **check** - completes checks before a command runs.
-   **command** - the command module that runs specific command tasks.
-   **core** - core modules that are required to run LinuxGSM.
-   **fix** - apply game server-specific fixes to allow the game server to run correctly.
-   **info** - gathers info from sources such as the OS and game server.
-   **install** - modules related to installation
-   **mods** - handles game server mods
-   **query** - game server query modules
-   **update** - handles updating of game servers and LinuxGSM

### Module Pointer

Some modules such as `fix.sh` and `check.sh` are made up of smaller tasks that are split up into sub-modules. Because of this, these modules become pointers for their sub-modules that will upon the sub-modules as required.

An example of this is when check.sh will be called within command_start.sh, it will automatically select which sub-module tasks are required and run them.

### Core Modules

Core modules handle vital are required by LinuxGSM. These include download, getopt, messages, exit, trap

### Module Order

Modules will launch in sequence as they are required by commands. The following modules will normally run in the following order when a command is executed:

```text
core
command
check
fix
```

It is possible to see the order that modules run by enabling `./gameserver dev`. Once enabled the module order will be saved in `dev-debug-function-order.log`

Example output of `./gameserver stop`

```text
+ core_functions.sh
++ core_legacy.sh
++ core_messages.sh
++ core_dl.sh
++ core_trap.sh
+ core_getopt.sh
+++ command_stop.sh
++++ check.sh
+++++ check_root.sh
+++++ check_tmuxception.sh
+++++ check_permissions.sh
+++++ check_system_dir.sh
+++++ check_logs.sh
+++++ check_deps.sh
++++++ info_distro.sh
+++++ check_config.sh
+++++ check_ip.sh
++++++ info_config.sh
++++++ info_parms.sh
+++++ check_status.sh
++++ info_config.sh
++++ check_status.sh
++++ check_status.sh
++++ check_status.sh
++++ check_status.sh
++++ core_exit.sh
```

## How Modules are Called

In bash to call another bash script, the `source` command is used. However, in LinuxGSM this is handled by the `core_modules.sh` module. This allows LinuxGSM to automatically download a module the first time it is used and then call the script.

To call a module simply add the name of the module file e.g `info_config.sh` and the module will be called. If a new module is being added it must be added to the list of modules in `core_functions.sh` like so.

```bash
info_config.sh(){
functionfile="${FUNCNAME}"
fn_fetch_function
}
```
