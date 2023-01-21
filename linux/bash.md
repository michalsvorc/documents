# Bash

- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
- [Bash best practices | cheat-sheets](https://bertvv.github.io/cheat-sheets/Bash.html)
- [How to Compare Strings in Bash](https://linuxize.com/post/how-to-compare-strings-in-bash/)
- [getopts](http://mywiki.wooledge.org/BashFAQ/035#getopts)

## Usage text

- [POSIX Utility Conventions](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html#tag_12_01)
- [Docopt language](http://docopt.org/)

Docopt: All elements are required by default, if not included in brackets "[ ]".

## exec

- [bash - What does an "exec" command do?](https://askubuntu.com/questions/525767/what-does-an-exec-command-do)

If you run exec > file, the redirection applies to the entire shell. Any output produced by the shell is written to file
instead of your terminal.

## Source functions from another shell script

```bash
. ./bin/_functions.sh --source-only
```
