# Adding a new Command

Adding new [commands](https://dev-docs.linuxgsm.com/technical/commands) to LinuxGSM is easier than you think and can be done in a few simple steps by following the instructions below.

## Create new command script

The first step is to create a new script in the `lgsm/modules` directory. The script should be named `command_[commandname].sh`, where `[commandname]` is the name of the command you want to add.

For example `lgsm/modules/command_hello_world.sh`:

```bash
#!/bin/bash
# LinuxGSM command_hello_world.sh module
# Author: Daniel Gibbs
# Contributors: http://linuxgsm.com/contrib
# Website: https://linuxgsm.com
# Description: Example Hello World command.

commandname="HELLO-WORLD"                                          # Identifies the command in code
commandaction="Hello World"                                        # Tells the user which command is running
moduleselfname="$(basename "$(readlink -f "${BASH_SOURCE[0]}")")"  # Used to get the filename of the current script
fn_firstcommand_set                                                # Track the first command executed

check.sh                                                           # Used to perform a variety of checks

# Place your code here
fn_print_info_nl "Hello World!"                                    # Print to console
fn_script_log_info "Hello World!"                                  # Log output of the script to the LinuxGSM log

core_exit.sh                                                       # Used to exit the script
```

## Add neccessary checks

You should ensure that any necessary [checks](https://dev-docs.linuxgsm.com/technical/checks) are run before or during the execution of the command. This is to ensure that the command (or parts of the command) can only be executed if the server is in a state where the command can do its job.

To do this, you need to add your command name to the `allowed_commands_array` in `lgsm/modules/check.sh` for each check you want LinuxGSM to perform.

Some Examples:

- The check `check_logs.sh` is needed by almost every command to check if log files exist:

```bash
allowed_commands_array=([...] HELLO-WORLD [...])
for allowed_command in "${allowed_commands_array[@]}"; do
    if [ "${allowed_command}" == "${commandname}" ]; then
        check_logs.sh
    fi
done
```

- You may want to check that the server is running before your command does anything:

```bash
allowed_commands_array=([...] HELLO-WORLD [...])
for allowed_command in "${allowed_commands_array[@]}"; do
    if [ "${allowed_command}" == "${commandname}" ]; then
        check_status.sh
    fi
done
```

- You can also run checks directly in your command script:

```bash
[...]

check_status.sh
if [ "${status}" == "1" ]; then
    fn_print_info_nl "Server Online"
else
    fn_print_info_nl "Server Offline"
fi


# Place your code here
fn_print_info_nl "Hello World!"                                    # Print to console
fn_script_log_info "Hello World!"                                  # Log output of the script to the LinuxGSM log

core_exit.sh                                                       # Used to exit the script
```

### Adding custom checks

If you need to add a custom check, you can do so by creating a new check script in `lgsm/modules` and using it either directly in your command script or by adding it to `lgsm/modules/check.sh` as shown above.

## Add your command to the list of commands

Now you need to have a look at the file `lgsm/modules/core_getopt.sh` and add your command to the list of commands. To do this, follow these last 2 steps:

### Add a new command array

This array should contain the following information

- `User commands` - The commands (short form & long form) that the user can type to run the command
- `Trigger comands` - The filename of the command
- `Description` - A short description of the command

For example:

```bash
cmd_hello_world=("hw;hello-world" "command_hello_world.sh" "Print Hello World!")
```

### Add the command array to the list of commands

Append the command array to the list of commands called `currentopt`. Do this wherever you think it makes sense. If your command has any conditions (e.g. only available for certain games), you should check for these conditions before adding the command to the list.

Some examples:

- If you want to make the command available for the game `examplegame`(`eg`):

```bash
# Hello World exclusive.
if [ "${shortname}" == "eg" ]; then
	currentopt+=("${cmd_hello_world[@]}")
fi
```

- If you want to make the command available for multiple games `examplegame`(`eg`) & `helloworldgame`(`hwg`):

```bash
# Hello World for examplegame and helloworldgame.
if [ "${shortname}" == "eg" ] || [ "${shortname}" == "hwg" ]; then
	currentopt+=("${cmd_hello_world[@]}")
fi
```

- If you want to make the command available for all games that use a particular game engine (e.g. `source'):

```bash
# Hello World for source engine games
if [ "${engine}" == "source" ]; then
    currentopt+=("${cmd_hello_world[@]}")
fi
```

- If you want to make the command available for all games

```bash
# Hello World
currentopt+=("${cmd_hello_world[@]}")
```
