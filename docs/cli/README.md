# How to write consistent CLIs?

On POSIX systems (e.g. Linux, MacOSX), it is recommended to use the [GNU](GNU coding conventions) and the [POSIX](POSIX guidelines). To summarize them:

- always handle `--version` and `--help`. Even shell utility programs like /bin/true accept these. `--help` is the first command anyone will try.

- Have the `--help` message list all the options. If the amount of options is more then a screen (55 lines), please refer to a man page or some form of documentation. List the default values of options and important environment variables. Show these option lists on argument error.

- use `--log-level` to set the verbosity of logging.

- accept `-a` short argument (single letter) and have some equivalent `--long-argument`, so `-a2`, `--long-argument=2`, `--long-argument 2` are equivalent. For rarely used options it is recommended to have `--only-long-argument` name.

- use - for standard input or output.

- use `--` as separator between options and file or other arguments

- mimic the behavior of similar programs by reusing most of their options conventions. In particular `-n` for dry run (à la make), `-h` for help, `-v` for verbosity.


Remember that on POSIX the shell is globbing arguments (before running your program!), so avoid requiring characters (like * or $ or ~) in options which would need to be shell-escaped.

# Style

From above examples, you might have noticed the options and arguments follow a certain style. We recommend to avoid `--arguments_that_have_underscores` and instead use `--arguments-with-dashes`.

[GNU]: https://www.gnu.org/prep/standards/standards.html#Command_002dLine-Interfaces
[POSIX]: http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html
