# Developing LinuxGSM

This page has been designed to help you learn how LinuxGSM code works.

As a user, it will allow you a better understanding of how LinuxGSM works. As a developer, it will help you with adding new servers, fixing bugs, and adding new features.

## Generalities

The LinuxGSM _executable_ `./gameserver` is the main entry point for users, their main interactions will be with this script. However, from a development perspective, this is only the gateway as it simply does the initial bootstrap and points to the commands and modules that are stored elsewhere. LinuxGSM is made up of many smaller (mainly bash) scripts (modules) that interact with each other to complete a set of tasks. A command will complete its set of tasks using the LinuxGSM modules.

## Main Executable

The main executable file `linuxgsm.sh` or `gameserver` is what the user interacts with to run commands.

`linuxgsm.sh` is designed to be used for the installation of a specific game server. You can run `./linuxgsm.sh install` to get a menu of the available servers or `./linuxgsm.sh gameserver` to install the specific game server.

To install a specific server `linuxgsm.sh` first downloads a complete list of all available servers from `serverlist.csv`. This file contains variables required to identify the server; `${gamename}`, `${shortname}` and `${servername}`. When installing a game server `linuxgsm.sh` copies itself using the`${servername}` variable as the script name and inserting the other variables into the copied file. The added variables allow LinuxGSM to know which server the user selected.

A user can also run the install again if they want multiple instances of the same server. This will give an output of `gameserver-2`,`gameserver-3` etc as the file name.

## Adding a new Game Server

Adding a new game server is one of the most common things developers do. This guide will help you add a new game server to LinuxGSM.

{% hint style="info" %}
replace gameserver with the name of the new server e.g rustserver
{% endhint %}

### Create new \_default.cfg config file

Firstly create a new `_default.cfg` file in `lgsm/config-default/config-lgsm/gameserver` . An existing \_default.cfg file can be used as a template.

Update all the variables in the new `_default.cfg` file to fit the new server.

Some common variables that will need updating:

* Add `## SteamCMD Login` section only if required.
* `startparameters` are any parameters the executable requires to run the game server.
* `appid`  used to download a game server from Steam. Remove if not using steam.
* \`steammaster\` used if the game servers are listed on the Steam master servers.
* `stopmode` defines how a server can safely exit.
* `querymode` defines the type of query monitor that can be used to check the server is responding.
* console type highlights to users if the console outputs and is interactive.
* Game Server Details `gamename` , `engine`, `glibc`.
* Various directory and config variables.

### Add the new server to serverlist.csv

Add the new server details to `serverlist.csv` as well as add any dependency requirements to all the distro csv files found in `lgsm/data` directory.

### Add any fixes to a fix file

Some game servers require alterations before they can start common examples include:

* copying library files to serverfiles
* symlinking files
* creating directories
* adding a directory to `LD_LIBRARY_PATH`

If this is required a fix module will need to be created.

1. Create a new module called `fix_[shortname].sh` (use an existing example as guidance)
2. Add the required fixes to the module
3. Add the module to `fix.sh`
4. Add the fix to `core_modules.sh` list

### Server Querying

Game servers can often be queried to check the server is running and return useful info. LinuxGSM uses gsquery.py to complete simple pings and [gamedig](https://github.com/gamedig/node-gamedig) to get detailed info returned in json format.&#x20;

Most game servers use the valve protocol for allowing queries, however, others are available. Look for any developer documentation to try and find out if querying is supported.&#x20;

Use the `query-raw` command to assist in testing the querying of the new game server.&#x20;

### Stop Mode

Game servers will be able to gracfully exit using various methods. Figure out the method the new game server uses. See [stop mode](https://docs.linuxgsm.com/features/stop-mode).

### Glibc Version

Most game servers require a minimum glibc version. Use the `detect-glibc` command to find out the minimum glibc version required

#### Functions, commands and script files

Script files are located in ${functionsdir}, which is ${rootdir}/lgsm/functions

* Every single script file must be declared in core\_functions.sh
* Commands are declared in core\_getopt.sh, depending on the game or engine

Note: You need to update those files with update-functions command after adding a new one.

#### Commands

Here are the command functions you might need to alter when adding a new server:

* command\_install.sh - Server installation must work properly
* command\_update.sh - if the given game supports updates (might required to add a file for that matter, for now, we use to add a single file for install and update, like for TeamSpeak 3).
* command\_details.sh - Server details need to be displayed properly
* command\_monitor.sh & monitor\_gsquery.sh, query\_gsquery.py & query\_gsquery.py - You'll need to read carefully and understand this code before altering it.
* core\_getopt.sh - You will define available commands in this one, displayed when the user runs `./gameserver` without an argument. Either use an existing opt or make a new one if needed.
* command\_start.sh & command\_stop.sh - Of course, your server needs to be able to start and stop properly.
* command\_debug.sh & command\_console.sh - Those commands usually work out of the box, but might require some more work. If not using tmux, then console should be disabled for this server in core\_getopt.sh.
* info\_config.sh - You might need to read variables out of configuration files such as Rcon information in the case of Squad.

#### Fixes

`command_install.sh` runs `fix.sh` at the end of server installation. If the given server requires a fix, then add `fix_gameserver.sh` and run it from `fix.sh`.

#### Core functions

**core\_dl.sh**

This is the first script to be run when `gameserver`is executed. This script allows for fetching LinuxGSM core files, but also for downloading big files within kind of an API.

**core\_functions.sh**

This is the second script to be run when `gameserver`is executed. This script declares all functions and fetches them when they are required.

**core\_getopt.sh**

This is the third and last script to be run when `gameserver`is executed. This script allows for setting and printing available commands to the user.

**core\_messages.sh**

This script allows for easy message output and logging. More details about it in the next part.

#### Messages & Logs

LGSM has a message/logging framework to avoid painful syntax into scripts.

Framework syntax is: `fn_print_whatever "This is your message"` If you want to replace the line afterwards, then reuse `fn_print_whatever`. If you want a new output on a new line, then use `fn_print_whatever_nl`. "nl" stands for "new line".

**On-Screen - Automated functions**

* \[ .... ] | fn\_print\_dots | fn\_print\_dots\_nl
* \[ OK ] | fn\_print\_ok | fn\_print\_ok\_nl
* \[ FAIL ] | fn\_print\_fail | fn\_print\_fail\_nl
* \[ ERROR ] | fn\_print\_error | fn\_print\_error\_nl
* \[ WARN ] | fn\_print\_warn | fn\_print\_warn\_nl
* \[ INFO ] | fn\_print\_info | fn\_print\_info\_nl

**On-Screen - Interactive messages**

* Print $gamename $commandaction and jump some lines | fn\_print\_header (used at the beginning of a command)
* Complete! |fn\_print\_complete | fn\_print\_complete\_nl
* Failure! | fn\_print\_failure | fn\_print\_failure\_nl
* Error! | fn\_print\_error2 | fn\_print\_error2\_nl
* Warning! | fn\_print\_warning | fn\_print\_warning\_nl
* Information! | fn\_print\_information | fn\_print\_information\_nl

**On-Screen End of Line**

* OK| fn\_print\_ok\_eol | fn\_print\_ok\_eol\_nl
* FAIL | fn\_print\_fail\_eol | fn\_print\_fail\_eol\_nl
* WARN | fn\_print\_warn\_eol | fn\_print\_warn\_eol\_nl
* FAIL | fn\_print\_info\_eol | fn\_print\_info\_eol\_nl
* QUERYING | fn\_print\_querying\_eol | fn\_print\_querying\_eol\_nl
* CHECKING | fn\_print\_checking\_eol | fn\_print\_checking\_eol\_nl
* CANCELED | fn\_print\_canceled\_eol | fn\_print\_canceled\_eol\_nl
* REMOVED | fn\_print\_removed\_eol | fn\_print\_removed\_eol\_nl
* UPDATE | fn\_print\_update\_eol | fn\_print\_update\_eol\_nl

**Logging**

Syntax: `fn_script_log "Message goes here."` Output: `## Feb 28 14:56:58 ut99-server: Monitor: Message goes here.`

* Simple action log | fn\_script\_log
* PASS (a successful test) | fn\_script\_log\_pass
* FATAL (an error has interrupted LGSM) | fn\_script\_log\_fatal
* ERROR | fn\_script\_log\_error
* WARN | fn\_script\_log\_warn
* INFO | fn\_script\_log\_info

#### Checks

Any script file must run `check.sh` at some point. Within `check.sh`, you will then choose what tests to run for a given function. The syntax of check.sh is a bit counter-intuitive: `local allowed_commands_array=( )` is the variable where you will enter the functions into which you need to run the following check.

There are several checks available:

* check\_config.sh checks for a missing config file or a wrong parameter.
* check\_deps.sh checks for missing dependencies and contains requirements
* check\_glibs.sh checks if the server has the correct Glibc version or a fix available.
* check\_ip.sh automatically identifies the server interface IP.
* check\_logs.sh checks if log files exist.
* check\_permissions.sh checks ownership & permissions of scripts, files and directories
* check\_root.sh checks if the user tried to run the script as root
* check\_status.sh checks the process status of the server. Either online or offline
* check\_steamcmd.sh checks if SteamCMD is installed correctly
* check\_system\_dir.sh checks if systemdir is accessible
* check\_system\_requirements.sh checks RAM requirements (maybe more into the future)
* check\_tmuxception.sh checks and prevents server start from tmux or screen

**core\_exit.sh**

This script allows for the use of exit codes which will print different outputs to LinuxGSM logs. Running `core_exit.sh` defaults exitcode variable to 0 which stands for a proper exit

* Normal exit: exitcode=0
* FATAL exitcode=1
* ERROR: exitcode=2
* WARN: exitcode=3

#### Server installation

Installing a new server is mainly done through two scripts:

* install\_server\_files.sh
* install\_config.sh

Sometimes, another script is required, such as for TeamSpeak 3: `update_ts3.sh`

#### Versioning

At the moment, only the main "gameserver" script has a version number. The syntax is pretty easy, it's all incremental, based on the date: `version="YYMMDD"`

### Testing and debugging your code

#### Working from your own GitHub branch

You will usually be developing onto your own repo. Using your own repo instead of the original one is quite easy.

1. Display your main "gameserver" file on GitHub, and select "Raw".
2. Make a test user, login to it
3. wget your Raw link and chmod +x the script.
4.  Edit your "gameserver" file by changing GitHub information to your username and repo and branch.

    ```bash
    ## Github Branch Select
    # Allows for the use of different function files
    # from a different repo and/or branch.
    githubuser="YourUsername"
    githubrepo="YourRepository"
    githubbranch="YourBranchName"
    ```

Now, any command you run will get your own GitHub files, and after any change you make on your repo, `./gameserver uf` will grab new files. If you make a change and that `./gameserver uf` don't get them, it means you were too quick, and that your curl still has old files in cache; in this case, you'll need to wait a few minutes to get your modifications.

#### How to test

You need to make sure that all needed commands displayed in opt work properly. So just run `./gameserver` to show available commands, then try commands one by one. A common procedure is to first work on command\_install, then start, then stop, then debug, then details, then monitor.

#### Oops, I found a bug!

If you found a bug, either you'll instantly know how to fix it, or you won't. And either it will be a bug caused by your own code or a bug into LinuxGSM itself. So let's address those cases.

1. It's caused by your own code parts and you know how to fix it: Just go on and fix it.
2. It's caused by your own code parts but you got no idea why: Use `./gameserver dev-debug` that will add a very detailed log into your rootdir that might help you figure this out. To disable the dev-debug mode, just re-run the command. If you still can't find why it's not working, come get help on Discord's #gsm-development channel or Github issue that might have been created for this issue.
3. You found a bug into LinuxGSM itself. First, you need to be sure that it's really a bug that affects every game, by testing with another game onto the original repo, otherwise, if it only affects your game, you will usually just need to add a clever conditional check to fix the issue.
