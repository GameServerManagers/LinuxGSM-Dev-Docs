# Exit Codes

Below is a list of exit codes and explanations for each code. An exit code hightights the state of the code once it has completed its task. This is used to highlight if the proccess completed, failed or somwhere inbetween.

to see the exit code you can activate developer mode.

```bash
./gameserver developer
```

## Types of Exit Codes

### Pass

-   **Code:** 0
-   **Description:** This code is returned when all is well.
-   **On Screen Automated:** \[ OK \]
-   **On Screen Interactive:** Complete!
-   **Logfile:** PASS

### Fatal

-   **Code:** 1
-   **Description:** Fatal errors occur when LinuxGSM is prevented from completing its task. e.g it was unable to start a server.
-   **On Screen Automated:** \[ FAIL \]
-   **On Screen Interactive:** Failure!
-   **Logfile:** FATAL

### Error

-   **Code:** 2
-   **Description:** An error occurs when LinuxGSM can complete its task however something went wrong. In many cases LinuxGSM will attempt to resolve errors itself.
-   **On Screen Automated:** \[ ERROR \]
-   **On Screen Interactive:** Error!
-   **Logfile:** ERROR

### Warning

-   **Code:** 3
-   **Description:** Warnings happen when there is something mis-configured or not setup correctly. LinuxGSM may still work but not do as expected.
-   **On Screen:** \[ WARN \]
-   **On Screen Automated:** \[ WARN \]
-   **On Screen Interactive:** Warning!
-   **Logfile:** WARN

### Info

-   **Code:** N/A
-   **Description:** Useful information about what LinuxGSM is currently doing.
-   **On Screen:**
-   **On Screen Automated:** \[ INFO \]
-   **On Screen Interactive:** Information!
-   **Logfile:** INFO

## How to use exit codes in code

An exit code is generated when you specify a logfile message e.g `fn_script_log_fatal`. When you want the script to exit you must use `core_exit.sh` rather than just the exit command. `core_exit.sh` will then handle the exit and specify the last known exit code. So if the more recent command was `fn_script_log_fatal` then the exit code will be 1

### Examples

```bash
fn_script_log_fatal "RCON password is not set"
core_exit.sh
```

This will exit with code 1

```bash
fn_script_log_error "RCON password is not set"
core_exit.sh
```

This will exit with code 2

```bash
fn_script_log_error "SteamCMD is missing"
LinuxGSM installs SteamCMD
fn_script_log_pass "SteamCMD has been installed"
core_exit.sh
```

This will exit with code 0
