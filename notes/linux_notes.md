# Linux Notes & Resources

# Basic Commands

- `find`
    - `find -name name.txt`
    - outputs `/dir/name.txt`
    - finds file with name / chosen extension

- `grep`
    - `grep "word" name.txt` searches for "word" within name.txt
    - outputs selected entry with "word" highlighted

- `wc`
    - `wc name.txt` returns wordcound of name.txt
    - outputs `100 name.txt`
    - word count

- operator `&`
    - runs the command in background

- operator `&&`
    - `command1 && command2` runs command2 only if command1 is successful

- operator `>`
    - redirects output of a command to a file; overwrites contents if file already exists
    - e.g. `echo newText > file` writes contents of file as "newText"

- operatoe `>>`
    - also an output redirector but instead appends output at the bottom of the file
    - e.g. `echo newLine >> file` adds "newLine" at the bottom of file without replacing its contents
