# Style Guide

In order to make LinuxGSM as coherent as possible, we adopted some code conventions to follow.\
Here are some of them.

## Variables

### Naming variables

Variables should be made of lowercase letters only and should be descriptive enough to understand its purpose (even if the variable is longer that preferred).

### Defining variables

Any variable should be defined through double quotes

```bash
var="value"
```

### Calling variables

Variable should always be called between brackets and double quotes to prevent globbing and word splitting.

```bash
echo "${var}"
```

## Directories

Directories are called using LinuxGSM directories variables, or relative to those. Common directory variables can be found in `linuxgsm.sh` and `_default.cfg` .

Examples:

```bash
mkdir -pv "${servercfgdir}"
mkdir -pv "${lgsmdir}/config-default/config-game"
du -sh "${rootdir}" 2> /dev/null
find "${executabledir}/bin"
```

## `if` Statements

If statements should look like the following

```bash
if [ "${shortname}" == "csgo" ];then
   # content
fi
```

if statements with multiple options like so

```bash
if [ "${shortname}" == "csgo" ]||[ "${shortname}" == "css" ]; then
   # content
fi
```

## Conditional checks

### Syntax

-   The `if [ statement ]; then` should be a one-liner operation.
-   Signs comparators like `==`, `lt`, `lt` etc. are preferred to `-eq`, `-le`, `-lt`.
-   Anything within an if statement must be tabulated one step deeper.

Example:

```bash
if [ "${test}" == "${var}" ]; then
    mycheck="true"
fi
```

### Expression Standards

Common if expressions LinuxGSM uses. More expressions [here](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html).

| Expression | Description                          |
| ---------- | ------------------------------------ |
| `-d`       | if directory exists                  |
| `! -d`     | if directory does not exist          |
| `-f`       | if file exists                       |
| `! -f`     | if file does not exist               |
| `-z`       | true if length of string is zero     |
| `-n`       | true if length of string is non-zero |
| `-v`       | true if the variable exists          |

{% hint style="danger" %}
Do not use `! -z` or `! -n`
{% endhint %}

There is a distinct difference between -n and -v.

\-n is used to check is a variable is set and not if it exists\
\-v is used to check if a variable exists and not it is set

```bash
var="set"
if [ -n "${var}" ]; then
 # Variable is set
fi
```

```bash
var=""
if [ -z "${var}" ]; then
 # Variable is not set
fi
```

```bash
var=""
# OR
var="set"
if [ -v var ]; then
 # Variable exista
fi
```

```bash
# var is missing
if [ ! -v var ]; then
 # Variable does not exist
fi
```

## Loops

-   Loops should be a one liner statement.
-   Anything within a loop must be tabulated one step deeper.

```bash
while [ "${var}" < "${cap}" ]; do
    echo "This is tabulated"
    let var=var+1
done
```

## Comments

As English is not always the native language of a developer, comments should use a formal writing style and be straight to the point. If unsure this short formal writing [guide](http://www2.ivcc.edu/rambo/tip_formal_writing_voice.htm) will help.

```bash
# Using comments help developers understand complex code, but should be used sparingly.
```

## Functions

-   Function should be named starting with `fn_` and using lowercase letters only.
-   Any recurrent task should be put into a function.
-   Anything within a function must be tabulated one step deeper.

Example:

```bash
fn_myfunction(){
    echo "This is tabulated"
}
```

## Messages

-   Messages should be given using core_messages.sh forms
-   Additional information messages are given in the form of `echo -e " * Message here"`

## Automated Messages

Automated messages are used with any commands that are non-interactive. Examples of this include Start, Stop and Monitor. There are various different alert messages available see [Exit-Codes](../technical/exit-codes.md) for details.

Each automated message starts with `fn_print_dots` to show a process is happening but with no known outcome.

### `fn_print_dots`

Once an outcome of a process is known the message uses an outcome message like `fn_print_ok` or `fn_print_fail`

```text
[ .... ] Starting fctrserver:
```

### `fn_print_ok`

```text
[  OK  ] Starting fctrserver: Factorio Server
```

The option of a newline is also available by appending `_nl` for example `fn_print_ok_nl`. This will add a carriage return to the message preventing it being overwritten by the next message.

```text
[  OK  ] Stopping fctrserver: Graceful: CTRL+c: 2: OK
[ .... ] Starting fctrserver: Factorio Server
```

### Characteristics of Automated Messages

Automated messages contain extra detail at the begining of the message that is pre-populated. Full stops must `not` be used with this type of message.

## Interactive Messages

Interactive messages are used with any commands that have interactive elements. Examples of this include Install, console and debug. There are various different alert messages available see \[\[Exit-Codes]] for details.

```text
Warning! If fctrserver is already running it will be stopped.
```

standard echo commands are normally used to supplement an alert or if an alert is not required. Bullet points can also be used

```bash
Information! Press "CTRL+b" then "d" to exit console.
Warning! Do NOT press CTRL+c to exit.
* https://docs.linuxgsm.com/commands/console
```

### Characteristics of Interactive Messages

Treat interactive messages as a standard sentence. All messages must begin with a capital and end with a full stop
