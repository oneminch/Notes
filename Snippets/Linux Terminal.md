## Commands

### File System

- `rm` - remove files or directories
- `touch filename` - create a file
- `ls` - list directory contents
    - `ls -a` - list all contents
    - `ls -l` - list all contents with detailed view
- `cat` - create, view and concatenate files
    - `cat > file` - create new file
    - `cat srcfile > destfile` - copy `srcfile` into `destfile`
- `less` - views the content of a file one screen at a time, allowing for scrolling.
- `mv src [src2 src3 ...] dir` - move src files to directory
    - `mv srcfile destfile` - rename src to destination
- `cp` - copy files or directories
    - `cp file1 file2`
    - `cp -r dir1 dir2` - copy all contents of `dir1` to `dir2`
- `pwd` - present working directory
- `diff file1.txt file2.txt` - compare file content differences
- `grep [OPTION...] PATTERNS [FILE...]` - search and print lines that match patterns
    - `-r` allows recursive searching through directories.
- `find DIR -name PATTERN` - search for file in a directory hierarchy
- `chmod` - change/modify file permissions
- `sort file` - sort lines of text files

- **Piping** (`|`) - take command and feed it to another
- **Redirection** (`>`) - write output to a file
    - e.g. `scoop list > scoop-installs.txt`

### Processes

- `ps` - displays information about currently running processes.
    - `ps aux` - detailed view.
- `kill` - terminates processes by their PID (Process ID). 
    - `kill -9` - forceful termination.
- `top` - provides a dynamic, real-time view of running processes and system resource usage.
- `htop` - interactive process viewer, with more user-friendly interface than `top`.

### Networking

- `ping` - tests connectivity to another host.
- `curl` - transfers data from or to a server, supporting various protocols. Useful for testing APIs.
- `scp` - securely copies files between hosts on a network.

### System Info

- `df -h` - displays disk space usage in a human-readable format.
- `du -sh` - summarizes disk usage of a directory.
- `free -m` - shows memory usage.
- `uname -a` - displays system information including kernel version and architecture.

### Miscellaneous

- `man` - user manual for any command
****- `history` - shows a list of previously executed commands, which can be useful for recalling complex commands.
- `sudo` - runs commands as the root user
    - `apt` - CLI for managing packages
        - `install` - install a package
        - `update` - checks to see which packages can be updated.
        - `upgrade` - performs the update for packages that can be updated

## Bash Scripting

- Number of arguments: `$#`
- All positional arguments (as a single word): `$*`
- All positional arguments (as separate strings): `$@`
- List array elements: `${array[*]}`

## Vim

- `vim filename` - edit a file via Vim
    - `i` - used to enter input mode.
    - `l` - moves the cursor to the right.
    - `h` - moves the cursor to the left.
    - `k` - moves the cursor up.
    - `j` - moves the cursor down.
    - `w` - place cursor after a word
    - `b` - jump to beginning of a word
    - `dd` - delete a line
    - `u` - undo a command
    - `dw` - delete word where cursor is located
    - `esc` - enter command mode
    - `:wq` - save and quit vim
    - `.` (period) - repeat a previous command

---
## Further

### Reads 📄

- [jlevy/the-art-of-command-line](https://github.com/jlevy/the-art-of-command-line)