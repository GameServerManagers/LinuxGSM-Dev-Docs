# Adding a new Game Server

Adding a new game server is one of the most common things developers do. This guide will help you add a new game server to LinuxGSM.

{% hint style="info" %}
replace gameserver with the name of the new server e.g rustserver
{% endhint %}

## Create new \_default.cfg config file

Firstly create a new `_default.cfg` file in `lgsm/config-default/config-lgsm/gameserver` . An existing \_default.cfg file can be used as a template.

Update all the variables in the new `_default.cfg` file to fit the new server.

Some common variables that will need updating:

-   Add `## SteamCMD Login` section only if required.
-   `startparameters` are any parameters the executable requires to run the game server.
-   `appid` used to download a game server from Steam. Remove if not using steam.
-   `steammaster` used if the game servers are listed on the Steam master servers.
-   `stopmode` defines how a server can safely exit.
-   `querymode` defines the type of query monitor that can be used to check the server is responding.
-   console type highlights to users if the console outputs and is interactive.
-   Game Server Details `gamename` , `engine`, `glibc`.
-   Various directory and config variables.

## Add the new server to serverlist.csv

Add the new server details to `serverlist.csv` as well as add any dependency requirements to all the distro csv files found in `lgsm/data` directory.

## Add any fixes to a fix file

Some game servers require alterations before they can start common examples include:

-   copying library files to serverfiles
-   symlinking files
-   creating directories
-   adding a directory to `LD_LIBRARY_PATH`

If this is required a fix module will need to be created.

1. Create a new module called `fix_[shortname].sh` (use an existing example as guidance)
2. Add the required fixes to the module
3. Add the module to `fix.sh`
4. Add the fix to `core_modules.sh` list

## Server Querying

Game servers can often be queried to check the server is running and return useful info. LinuxGSM uses gsquery.py to complete simple pings and [gamedig](https://github.com/gamedig/node-gamedig) to get detailed info returned in json format.&#x20;

Most game servers use the valve protocol for allowing queries, however, others are available. Look for any developer documentation to try and find out if querying is supported.&#x20;

Use the `query-raw` command to assist in testing the querying of the new game server.&#x20;

## Stop Mode

Game servers will be able to gracefully exit using various methods. Figure out the method the new game server uses. See [stop mode](https://docs.linuxgsm.com/features/stop-mode).

## Glibc Version

Most game servers require a minimum glibc version. Use the `detect-glibc` command to find out the minimum glibc version required.

## Details

Various game server info will need to be parsed from game server configs or variables. Use the info\_\*.sh modules to add this info.&#x20;

## Custom Updater

Not all game servers use SteamCMD. If this is the case a custom update module will need to be created. There are a number of examples in the code that can be used as a baseline.

## Custom Commands

Some game servers may require bespoke commands to complete tasks. Examples of this include Teamspeak 3 and Unreal Tournament 2004. Take a look at the `core_getopts.sh` module for examples of how to add commands.
