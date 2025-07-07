# brename
## Requirements
Tcl, tcllib. I use Tcl 9.0, but it should work with 8.6 too.
## Usage
brename ?options? \<dir\> \<name_pattern\> \<rename_pattern\>
+ dir -- directory containing files you want to rename
+ name_pattern -- regexp to match file names
+ rename_pattern -- regexp to rename matched files

options:
+ -r -- Descend the directories. Will recursively traverse any encountered directories.
<!-- TODO: specify recursion depth) -->
+ -l -- Follow links. Same as above, but for links.
+ -t value -- Types of matched files to rename. `value` is one of three chars (*f* file, *d* directory, *l* link), or a list of any of them If used with `-l` or `-d`, matched links and dirs will first be descended, and then renamed.
+ -v -- Print matches. Will print which files are being renamed.
+ -p -- Dry run. Do not rename matched files. Useful with `-v` to look at the matches.

Tcl `cmdline` automatically generates `-help` / `-?` and `--` options. For regexp syntax, see [re_syntax](https://www.tcl-lang.org/man/tcl8.6.13/TclCmd/re_syntax.htm).

## BRENAME_JSON
When this environment variable is *true*, brename will print errors and usage help in JSON format. Useful for automation with scripts, integration to other utilities, or generating shell autocompletion files.
<!-- TODO: generalise usage-json into a Tcl package for use in other tools -->

## Examples
> `brename -t=f -v ./mytclx/unix 'tclX(.+\.c)' 'MyTclX\1'`

Match all C files beginning with **tclX** and replace **tclX** with **MyTclX**. (parens) is a regexp capture group. You can specify many of them and reference numerically -- `\1` `\2` `\3`, -- as per usual.

## Afterword

Any input is encouraged. If you notice a bug, please file an issue.