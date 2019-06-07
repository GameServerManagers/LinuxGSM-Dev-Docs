# Functions



Functions allow the grouping of code to allow it to be called as many times as required, this prevents replicating the same code over and over.

## LinuxGSM Functions

All functions within LinuxGSM begin with an `fn_` and should be descriptive of what the function is doing. Words are separated by an underscore `_`.

Examples

```text
fn_stop_graceful_cmd
```

```text
fn_update_ts3_dl
```

### Syntax

All functions should be formated with the following syntax.

```text
fn_function_name(){
  code
}
```

