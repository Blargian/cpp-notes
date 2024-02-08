
| Description  | Command  |
|---|---|
| adds a breakpoint on line __  | `break 69`  |
| adds a breakpoint in file on line __  | `break main:57`  |
| removes a breakpoint on line_  | `clear 69`  |
| show source layout  | `layout src`  |
| set cmd args apropos | `set args`   |
| enable tui mode  | `tui enable`  |
| temporary breakpoint  | `tb 5`  |
| run to line  | `until 5`  |
| show output in a different terminal  | `set inferior-tty`  |
| (windows only) show output in a different terminal  | `set new-console on`  |
# LLDB Commands

| Description | Command |
| ---- | ---- |
| launch lldb with arguments | `lldb file -- arg1` |
| launch lldb | `run`  |
| adds a breakpoint on line __ | `breakpoint set 57` |
| adds a breakpoint in file on line __ | `breakpoint set --file x --line ` |
| set a breakpoint on a function | `breakpoint set --name foo ` |
| to see std::str when print() gives the Summary Unavailable error  | `frame variable --flat varname` |
| list all breakpoints | `breakpoint list` |
| delete all breakpoint | `br delete` |
|  |  |
|  |  |
|  |  |
|  |  |