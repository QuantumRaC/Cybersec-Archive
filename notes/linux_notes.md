# Linux Notes & Resources

# (Very) Basic Commands

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
