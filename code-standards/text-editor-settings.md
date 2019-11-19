---
description: '[WIP] discuss using LF and white space remover etc.'
---

# Text Editor Settings

Below is information on requirements needed when using a text editor to work on LinuxGSM code. All the reccomended text editors can be setup to take in to account the requriements.

* [Atom ](https://atom.io/)\(recommended\)
* [Sublime Text](https://www.sublimetext.com/)
* [Notepad++](https://notepad-plus-plus.org/)

## Indentation

LinuxGSM uses `tabs` instead of spaces, it is possible to specify tabs and convert spaces to tabs if required.

## Line Ending

All files must be saving using `LF` \(Line Feed\) line endings which if the line ending used by UNIX based systems. Please ensure that your text editor is saving in `LF` format as failure to do so will cause BASH scripts to stop functioning.

For more info about line endings check out the article "[The Great Newline Schism](https://blog.codinghorror.com/the-great-newline-schism/)".

## Trailing White Spaces

When developing code somtimes it can be easy to end up with trailing white spaces. as shown below.

```text
fn_example_func(){
    # The line below has two spaces after its final character
    code••
}
```

All code must have whitespaces removed to keep code tidy. Many text editors have a feature that will automaticly remove trailing whitespaces when a file is saved. It is highly reccomended this feature is turned on.

