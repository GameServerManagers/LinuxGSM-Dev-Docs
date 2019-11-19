# Style Guide

In order to make LinuxGSM as coherent as possible, we adopted some code conventions to follow.  
Here are some of them.

## Variables

#### Naming variables

Variables should be made of lowercase letters only.

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

### Directories

Directories are called using LinuxGSM directories variables, or relative to those.

Examples:

```bash
cp "config.cfg" "${servercfgfullpath}"
find "${executabledir}/bin"
```

## `if` Statements

If statements should look like the following

```text
if [ "${shortname}" == "csgo" ];then
   # content
fi
```

if statements with multiple options like so

```text
if [ "${shortname}" == "csgo" ]||[ "${shortname}" == "css" ]; then
   # content
fi
```

## Conditional checks

### Syntax

* The `if [ statement ]; then` should be a one-liner operation.
* Signs comparators like `==`, `lt`, `lt` etc. are prefered to `-eq`, `-le`, `-lt`.
* Anything within an if statement must be tabulated one step deeper.

Example:

```bash
if [ "${test}" == "${var}" ]; then
    mycheck="true"
fi
```

### Expression Standards

#### Avoid `! -z`and `! -n`

`-z` true if the length of string is zero. `-n` True if the length of string is non-zero.

#### To check `var` exists Use `-v`

Use the `-v` expression to check a var exists instead of `-z` and `-n` as it is specifically designed to check if a var exists

> note: although -v is preferred sometimes -z is required to get the correct results.

`-v` True if the shell variable varname is set \(has been assigned a value\).

```bash
if [ -v varname ]; then
 # Variable exists
fi
```

```bash
if [ ! -v varname ]; then
 # Variable does not exist
fi
```

`-v` does not have an opposite so the `! -v` needs to be used.

## Loops

* Loops should be a one liner statement.
* Anything within a loop must be tabulated one step deeper.

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

* Function should be named starting with `fn_` and using lowercase letters only.
* Any recurrent task should be put into a function.
* Anything within a function must be tabulated one step deeper.

Example:

```bash
fn_myfunction(){
    echo "This is tabulated"
}
```

## Messages

* Messages should be given using core\_messages.sh forms
* Additional information messages are given in the form of echo " \* Message here"

## Automated Messages

Automated messages are used with any commands that are non-interactive. Examples of this include Start, Stop and Monitor. There are various different alert messages available see \[\[Exit-Codes\]\] for details.

Each automated message starts with fn\_print\_dots to show a process is happening but with no known outcome.

fn\_print\_dots

```text
[ .... ] Starting fctrserver:
```

Once an outcome of a process is known the message uses an outcome message like `fn_print_ok` or `fn_print_fail`

fn\_print\_ok

```text
[  OK  ] Starting fctrserver: Factorio Server
```

The option of a newline is also available by appending `_nl` for example `fn_print_ok_nl`. This will add a carriage return to the message preventing it being overwritten by the next message.

```text
[  OK  ] Stopping fctrserver: Graceful: CTRL+c: 2: OK
[ .... ] Starting fctrserver: Factorio Server
```

#### Characteristics

Interactive messages contain extra detail at the begining of teh message that is pre-populated. Full stops must `not` be used with this type of message.

### Interactive Messages

Interactive messages are used with any commands that have interactive elements. Examples of this include Install, console and debug. There are various different alert messages available see \[\[Exit-Codes\]\] for details.

```text
Warning! If fctrserver is already running it will be stopped.
```

standard echo commands are normally used to supplement an alert or if an alert is not required. Bullet points can also be used

```text
Information! Press "CTRL+b" then "d" to exit console.
Warning! Do NOT press CTRL+c to exit.
* https://docs.linuxgsm.com/commands/console
```

#### Characteristics

Treat interactive messages as a standard sentence. All messages must begin with a capital and end with a full stop

