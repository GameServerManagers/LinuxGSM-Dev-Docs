# Functions

Functions are groupings of code that complete a task \(function\). These functions can be called upon anywhere within the code. Creating a function prevents having to replicat the same code over and over.

## LinuxGSM Functions

All functions within LinuxGSM begin with an prefix `fn_` and should be descriptive of what the function is doing. Words are separated by an underscore `_`. 

For LinuxGSM development, it is important that developers understand what a function does which is why all function names must describes the propose of the function. A longer function name that describes the function is prevered over a short one that does not. 

### Examples

```text
fn_stop_graceful_cmd
```

```text
fn_update_ts3_dl
```

### Syntax

All functions should be formatted with the following syntax.

```text
fn_function_name(){
    code
}
```

