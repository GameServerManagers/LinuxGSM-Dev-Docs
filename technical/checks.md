# Checks

Any script file must run `check.sh` at some point. Within `check.sh`, you will then choose what tests to run for a given function. The syntax of check.sh is a bit counter-intuitive: `local allowed_commands_array=( )` is the variable where you will enter the functions into which you need to run the following check.

There are several checks available:

-   check_config.sh checks for a missing config file or a wrong parameter.
-   check_deps.sh checks for missing dependencies and contains requirements
-   check_glibs.sh checks if the server has the correct Glibc version or a fix available.
-   check_ip.sh automatically identifies the server interface IP.
-   check_logs.sh checks if log files exist.
-   check_permissions.sh checks ownership & permissions of scripts, files and directories
-   check_root.sh checks if the user tried to run the script as root
-   check_status.sh checks the process status of the server. Either online or offline
-   check_steamcmd.sh checks if SteamCMD is installed correctly
-   check_system_dir.sh checks if systemdir is accessible
-   check_system_requirements.sh checks RAM requirements (maybe more into the future)
-   check_tmuxception.sh checks and prevents server start from tmux or screen
