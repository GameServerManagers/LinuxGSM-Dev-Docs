# Messages & Logs

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
