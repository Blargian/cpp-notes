| Description                                                                                                                          | Command                                            |
| ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------- |
| find path of g++ or gcc                                                                                                              | `which g++`                                        |
| check if you are admin or not                                                                                                        | net session                                        |
| change directory                                                                                                                     | `cd`                                               |
| list files in directory                                                                                                              | `ls`                                               |
| list all files in directory (hidden ones)                                                                                            | `ls -a`                                            |
| create temporary cmd variable ... if you want to make it permanent, for a non interactive shell you'll need to add it to `~/.bashrc` | `export VAR=`                                      |
| use temporary variable                                                                                                               | `$VAR`                                             |
| print to terminal                                                                                                                    | `echo`                                             |
| `echo` omit newline from output                                                                                                      | `echo -n`                                          |
| `echo` enable the function of backslash (escaping)                                                                                   | `echo -e`                                          |
| show kind of file                                                                                                                    | `file`                                             |
| show file with line endings. This displays Unix line endings (`\n` or LF) as `$` and Windows line endings (`\r\n` or CRLF) as `^M$`. | `cat -e filename.txt`                              |
| Convert betweeen unix and dos line endings                                                                                           | `dos2unix filename.txt` or `unix2dos filename.txt` |
| change file and group permissions https://www.linode.com/docs/guides/modify-file-permissions-with-chmod/                             | `chmod`                                            |
| netcat - reads and writes data across network connections                                                                            | `nc [options] host port`                           |
| File descriptor 1 is the standard output (`stdout`).  <br>File descriptor 2 is the standard error (`stderr`).                        | `2>&1` -> redirects stderr to stdout               |
| indicates that what follows and precedes is a _file descriptor_, and not a filename                                                  | `&`                                                |
|                                                                                                                                      |                                                    |
## Vim specific
| Description | Command |
| ---- | ---- |
| show lines in vim | `: set number` |
| cut a line | `d` |
| enter visual block mode (for copying) | `v` |
| undo | `u` |
| copy | `y` |
|  |  |

## Curl specific
| Description |  |
| ---- | ---- |
| posts data exactly as specified with no extra processing whatsoever  | `curl --data-binary <data>` |
| send the file after this character as the body of the POST request | `@` |
| from stdin. | `-` |
| send from stdin | `@-` |
|  |  |
|  |  |