# Checks

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
