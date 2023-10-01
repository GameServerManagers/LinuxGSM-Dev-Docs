# Commands

Within LInuxGSM there are many commands that a user will run to complete tasks such as start, stop, monitor, and details. Command scripts are stored will all other modules and are always named something like `command_install.sh`.

Here are the command functions you might need to alter when adding a new server:

* command\_install.sh - Server installation must work properly
* command\_update.sh - if the given game supports updates (might required to add a file for that matter, for now, we use to add a single file for install and update, like for TeamSpeak 3).
* command\_details.sh - Server details need to be displayed properly
* command\_monitor.sh & monitor\_gsquery.sh, query\_gsquery.py & query\_gsquery.py - You'll need to read carefully and understand this code before altering it.
* core\_getopt.sh - You will define available commands in this one, displayed when the user runs `./gameserver` without an argument. Either use an existing opt or make a new one if needed.
* command\_start.sh & command\_stop.sh - Of course, your server needs to be able to start and stop properly.
* command\_debug.sh & command\_console.sh - Those commands usually work out of the box, but might require some more work. If not using tmux, then console should be disabled for this server in core\_getopt.sh.
* info\_config.sh - You might need to read variables out of configuration files such as Rcon information in the case of Squad.
