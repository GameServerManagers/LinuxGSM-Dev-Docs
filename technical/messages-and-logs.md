# Messages & Logs

LGSM has a message/logging framework to avoid painful syntax into scripts.

Framework syntax is: `fn_print_whatever "This is your message"` If you want to replace the line afterwards, then reuse `fn_print_whatever`. If you want a new output on a new line, then use `fn_print_whatever_nl`. "nl" stands for "new line".

## On-Screen - Automated functions

-   [ .... ] | fn_print_dots | fn_print_dots_nl
-   [ OK ] | fn_print_ok | fn_print_ok_nl
-   [ FAIL ] | fn_print_fail | fn_print_fail_nl
-   [ ERROR ] | fn_print_error | fn_print_error_nl
-   [ WARN ] | fn_print_warn | fn_print_warn_nl
-   [ INFO ] | fn_print_info | fn_print_info_nl

## On-Screen - Interactive messages

-   Print $gamename $commandaction and jump some lines | fn_print_header (used at the beginning of a command)
-   Complete! |fn_print_complete | fn_print_complete_nl
-   Failure! | fn_print_failure | fn_print_failure_nl
-   Error! | fn_print_error2 | fn_print_error2_nl
-   Warning! | fn_print_warning | fn_print_warning_nl
-   Information! | fn_print_information | fn_print_information_nl

## On-Screen End of Line

-   OK| fn_print_ok_eol | fn_print_ok_eol_nl
-   FAIL | fn_print_fail_eol | fn_print_fail_eol_nl
-   WARN | fn_print_warn_eol | fn_print_warn_eol_nl
-   FAIL | fn_print_info_eol | fn_print_info_eol_nl
-   QUERYING | fn_print_querying_eol | fn_print_querying_eol_nl
-   CHECKING | fn_print_checking_eol | fn_print_checking_eol_nl
-   CANCELED | fn_print_canceled_eol | fn_print_canceled_eol_nl
-   REMOVED | fn_print_removed_eol | fn_print_removed_eol_nl
-   UPDATE | fn_print_update_eol | fn_print_update_eol_nl

## Logging

Syntax: `fn_script_log "Message goes here."` Output: `## Feb 28 14:56:58 ut99-server: Monitor: Message goes here.`

-   Simple action log | fn_script_log
-   PASS (a successful test) | fn_script_log_pass
-   FATAL (an error has interrupted LGSM) | fn_script_log_fatal
-   ERROR | fn_script_log_error
-   WARN | fn_script_log_warn
-   INFO | fn_script_log_info
