# Linux Notes & Resources

# (Very) Basic Commands

- `ls`
  - lists the contents of the working directory
  - `ls -a` (`-a` is short for `--all`) shows hidden folders (those that beging with `.`)
  - `-h` for human readeable format
  - `-l` for long output including read-write permissions and dates

- `touch`
  - `touch newFile` creates newFile under current dir

- `mkdir`
  - `mkdir mydirectory` creates mydirectory under current dir

- `rm`
  - `rm file` removes file; `rm -R directory` removes directory

- `cp`
  - copies the entire contents of an existing file into a new file
  - `cp note note2` copies note to note2

- `mv`
  - instead of creating a new file, the original file is merged
  - can be used to move or rename file/folders
  - `mv file1 file2` renames file1 to file2

- `file`
  - determines file type
  - `file note` -> `note: ASCII text`

- `find`
    - e.g. `find -name name.txt`
    - outputs `/dir/name.txt`
    - finds file with name / chosen extension

- `grep`
    - e.g. `grep "word" name.txt` searches for "word" within name.txt
    - outputs selected entry with "word" highlighted

- `wc`
    - e.g. `wc name.txt` returns wordcound of name.txt
    - outputs `100 name.txt`
    - word count

# Users

- `su`
  - switches between users
  - need password unless you are the root user
  - `su username`

# Network-Related

- `ssh`
  - e.g. `ssh racc@10.10.10.10` logs in as user racc with target IP using [SSH](notes.md#ssh-secure-shell
)

# Operators

- operator `&`
    - runs the command in background

- operator `&&`
    - `command1 && command2` runs command2 only if command1 is successful

- operator `>`
    - redirects output of a command to a file; overwrites contents if file already exists
    - e.g. `echo newText > file` writes contents of file as "newText"

- operator `>>`
    - also an output redirector but instead appends output at the bottom of the file
    - e.g. `echo newLine >> file` adds "newLine" at the bottom of file without replacing its contents

# Files & Directories

- `/etc`
  - important root directory
  - commonplace location to store system files
  - **`sudoers.d`**: contains a list of users & groups that have permission to run sudo
  - **`passwd`** & **`shadow`**: shows how the system stores passwords for each user encrypted in sha512
- `/var`
  - stores data frequently accessed / written by services / applications
    - e.g. `/var/log/` - log files from running services / apps
- `/root`
  - home directory for the "root" system user
- `/tmp`
  - volatile and used to store data that only needs to be accessed once or twice
  - contents cleared out once computer restarts
  - **any user can write to this folder by default**; good place to store things like enumeration scripts