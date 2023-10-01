# Main Executable

The LinuxGSM _executable_ `./gameserver` is the main entry point for users, their main interactions will be with this script. However, from a development perspective, this is only the gateway as it simply does the initial bootstrap and points to the commands and modules that are stored elsewhere. LinuxGSM is made up of many smaller (mainly bash) scripts (modules) that interact with each other to complete a set of tasks. A command will complete its set of tasks using the LinuxGSM modules.

The main executable file `linuxgsm.sh` or `gameserver` is what the user interacts with to run commands.

`linuxgsm.sh` is designed to be used for the installation of a specific game server. You can run `./linuxgsm.sh install` to get a menu of the available servers or `./linuxgsm.sh gameserver` to install the specific game server.

To install a specific server `linuxgsm.sh` first downloads a complete list of all available servers from `serverlist.csv`. This file contains variables required to identify the server; `${gamename}`, `${shortname}` and `${servername}`. When installing a game server `linuxgsm.sh` copies itself using the`${servername}` variable as the script name and inserting the other variables into the copied file. The added variables allow LinuxGSM to know which server the user selected.

A user can also run the install again if they want multiple instances of the same server. This will give an output of `gameserver-2`,`gameserver-3` etc as the file name.
