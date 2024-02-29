# ShellCheck Linter

## Introduction

In addition to following our style guide, we recommend using ShellCheck linter. ShellCheck is a powerful tool for analyzing and improving your shell scripts. It can detect syntax errors, common mistakes, and potential bugs in your scripts, providing suggestions that improve both the safety and the performance of your code.

## Why ShellCheck?

ShellCheck offers several benefits for shell script development, including:

- **Detection of Syntax Errors**: Quickly identifies and helps you fix syntax issues that could cause your script to fail.
- **Best Practices Enforcement**: Suggests modifications to make your script more robust and reliable, following industry best practices.
- **Improved Readability**: Offers suggestions to make your script more readable and maintainable.
- **Portability Advice**: Warns about constructs that are not supported in all shells, helping you write more portable scripts.

Examples of bad code that ShellCheck can help to catch and fix can be found at [ShellCheck's Gallery of Bad Code](https://github.com/koalaman/shellcheck?tab=readme-ov-file#gallery-of-bad-code).

## Installing ShellCheck

While [ShellCheck](https://github.com/koalaman/shellcheck) can be installed and used in various environments (Linux, macOS, Windows, and online), for developers using Visual Studio Code, the preferred method is installing the [ShellCheck VSCode extension](https://marketplace.visualstudio.com/items?itemName=timonwong.shellcheck). This extension integrates ShellCheck directly into your IDE, streamlining your workflow.

### Installing ShellCheck Extension in Visual Studio Code

1. **Open Visual Studio Code**.
2. Navigate to the **Extensions view** by clicking on the square icon on the sidebar, or pressing `Ctrl+Shift+X`.
3. In the search bar, type `shellcheck` to find the extension.
4. Look for the extension named `ShellCheck` by `timonwong`, which should be the top result.
5. Click **Install** to add the extension to your Visual Studio Code.

### Configuring ShellCheck Extension

After installation, the ShellCheck extension should work out of the box with default settings. However, you can customize its behavior via settings:

- To access the settings, go to **File > Preferences > Settings** (or `Ctrl+,`), search for `ShellCheck`, and adjust as needed.
- You can specify custom paths to the ShellCheck binary, exclude specific warnings, or change the severity of issues reported by ShellCheck.

## Using ShellCheck

With the ShellCheck extension installed, your shell scripts will be automatically linted as you write them. Issues will be highlighted in the editor, and you can hover over them to see detailed descriptions and suggestions. This immediate feedback helps you write better scripts faster.
