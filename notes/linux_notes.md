## 📚 Table of Contents

- [Linux Notes \& Resources](#linux-notes--resources)
- [(Very) Basic Commands](#very-basic-commands)
- [Processes](#processes)
- [Users](#users)
- [Networks](#networks)
- [Operators](#operators)
- [Shells](#shells)
- [Modules](#modules)
- [Package Management](#package-management)
- [Files \& Directories](#files--directories)

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

- `cp`&`scp`
  - (securely) copies the entire contents of an existing file into a new file
  - `cp note note2` copies note to note2
  - `scp user@10.10.10.10:8000/home/user/doc.txt notes.txt` copies file from remote computer (not logged into)'s port 8000 to local notes.txt

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



# Processes
- for concept see [processes](notes.md#processes) 

- `ps`
  - provides list of running processes as current user's session
  - additional info (status code, session, CPU usage time, name of command being executed)
  - `ps aux` allows viewing processes run by other users & those that don't run from a session (i.e. system processes)

- `top`
  - real-time stats about processes running on system
  - refreshes once every 10 seconds / when using arrow keys to browse

- `kill`
  - `kill 1337` kills PID 1337
  - signals to send to process when it's killed:
    - `SIGTERM` kills but allow it to do some cleanup tasks beforehand
    - `SIGKILL` kills and doesn't do any cleanup
    - `SIGSTOP` stops / suspends a process

- `systemctl`
  - allows interaction with the systemd process / daemon
  - `systemctl [option] [service]`
    - options: `start`, `stop`, `enable`, `disable`
    - `start` and `stop` switches it on and off immediately but does not affect auto-start at boot
    - `enable` and `disable` doesn't immediately switch it on and off but enables / disables auto-start at boot
- `fg`
  - brings the background process back into use (foreground) on the terminal

- `crontab`
  - used to schedule repetitive tasks via the `cron` daemon
  - jobs are defined in a crontab file using a 5-field time format followed by the command:
    - `* * * * * command`
    - `│ │ │ │ └── day of week (0-7, Sunday = 0 or 7)`
    - `│ │ │ └──── month (1-12)`
    - `│ │ └────── day of month (1-31)`
    - `│ └──────── hour (0-23)`
    - `└────────── minute (0-59)`
  - use `crontab -e` to edit the current user's crontab
  - `crontab -l` to list scheduled tasks
  - `crontab -r` to remove
  - e.g. `0 2 * * * /home/user/backup.sh` runs backup script every day at 2:00 AM at the timezone & time of the machine
  - `@reboot command` runs at reboot
  - See conceptual overview in [notes.md – cron / crontab](notes.md#cron--crontab)



# Users

- `su`
  - switches between users
  - need password unless you are the root user
  - `su username` switches to username
  - `sudo su` becomes root user

# Networks

- `ssh`
  - e.g. `ssh racc@10.10.10.10` logs in as user racc with target IP using [SSH](network_notes.md#ssh-secure-shell)
  - runs on **port 22**
  - `ssh hostname` if username is same as logged-in username
  - argument `-X` required to support running graphical interfaces
  
- `telnet`
  - see [Telnet](network_notes.md#telnet)

- `wget`
  - allows downloading files from the web via HTTP
  - `wget https://url/file.txt`
  - `wget -O output.txt https://file.txt`

- `nmap`
  - stands for **Network Mapper**
  - scans hosts and networks to discover open ports, running services, OS info, and firewall rules
  - useful for diagnostics, network mapping, and security auditing
  - Common usage:
    - `nmap -p 22 <ip>` – check if SSH port is open
    - `nmap <ip>` – quick scan of the most common 1000 TCP ports
    - `nmap -p- <ip>` – scan all 65535 TCP ports
    - `nmap -sV <ip>` – detect service versions
    - `nmap -O <ip>` – attempt OS detection
    - `nmap -sn <ip-range>` – ping scan, shows which hosts are online

- `nslookup [url]`
  - looks up the domain's IP addr

- `ip address show`
  - `ip a s` - lists the available network interfaces

- `libpcap` library
  - `tcpdump`
    - basic packet capture
      - `-i INTERFACE` - listens to a specific interface; or `-i any` `-i eth0`
        - `ip`/`ip6`/`udp`/`tcp`/`icmp` - add protocol name after `INTERFACE` to filter by protocol
      - `-w FILE` - saves captures packets to file (.pcap)
      - `-r FILE` - reads packets from a file
      - `-c COUNT` - specifies the number of packets to capture; without specifying, it continues til interruption
      - `-n` - stops resolving IP addr with DNS lookup
        - `-nn` stops both DNS and port number lookup (resolves port number into port name (e.g. 80 to http))
      - `-v` - to produce a slightly more verbose output; adds TTL, identification, total length & options in IP packets, etc.
        - `-vv` is more verbose, `-vvv` even more verbose
      - `host IP`/`host HOSTNAME` - e.g. example.com - listens to packets exchanged with specific host
        - `src host IP`/`src host HOSTNAME` or `dst host IP`/`dst host HOSTNAME`
      - `port PORT_NUMBER` - filters by port
        - `src port PORT_NUMBER` or `dst port PORT_NUMBER`
    - **logical arguments (and, or, not) work in `tcpdump`.**
    - filtering
      - `greater LENGTH`/`less LENGTH` - filters packets with greater or equal to / less than or equal to specified length
      - **header bytes**:
        - tcp allows referring to contents of any byte in the header with `proto[expr:size]` 
          - (proto is protocol; expr indicates byte offset starting at 0; size (optional) is the number of bytes we want to examine)
          - can use binary operations
          - `tcp[tcpflags]` refer to the TCP flags field
            - `tcpflags` i.e. `tcp-syn`, `tcp-ack`, `tcp-fin`, `tcp-rst`, `tcp-push`
          - e.g. `tcpdump "tcp[tcpflags] == tcp-syn` captures TCP packets with only the SYN flag set and all other flags unset
            - `tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"` captures TCP packets with at least the SYN or ACK flag set
    - displaying packets
      - `-q` quick output that prints timestamp, src and dst IP addr & port number
      - `-e` prints link-level header (i.e. includes MAC addr in output)
      - `-A` shows packet data in ASCII
      - `-xx` shows packet data in hex
      - `-X` shows packet headers and data in hex and ASCII

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

# Shells

- `echo $SHELL` shows which shell you're using
  - `/etc/shells` contains all installed shells on a Linux system
  - `.chsh -s /usr/bin/zsh` permanently changes default shell to `zsh`

- Shells
  - **Bash (Bourne Again Shell)**
    - default for most Linux distributions
    - in the middle of completing a command, tab key automatically completes the command or gives suggestions
    - keeps a history file & logs all commands
      - `history` displays all previous commands
  - **Fish (Friendly Interactive Shell)**
    - very simple syntax & auto spell correction for commands
    - limited scripting features
  - **Zsh (Z Shell)**
    - modern shell with tab completion & command history functionality
    - capable of writing scripts
    - extensive customization makes it slower than other shells

# Modules

- `HTTPServer`
  - `python3 -m http.server` to start server using module
  - serves on a specific port from machine's IP

# Package Management

- `apt`
  - manages software packages on Debian-based systems (e.g. Ubuntu)
  - automatically handles dependencies and retrieves packages from online repo
  - common commands:
    - `sudo apt update` – updates local package index
    - `sudo apt upgrade` – upgrades all upgradable packages
    - `sudo apt install <pkg>` – installs specified package
    - `sudo apt remove <pkg>` – removes specified package (keeps config)
    - `sudo apt purge <pkg>` – removes package and its config files
    - `sudo apt autoremove` – cleans up unused packages


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