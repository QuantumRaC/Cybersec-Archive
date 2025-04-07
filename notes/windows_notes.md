# Windows OS Notes

- Current version of Windows Server OS = **Windows Server 2019**
- After October 5th 2021 - **Windows 11** for end-users

## Windows 11 Home vs Pro (Security-wise)

  - **BitLocker**
    - *Pro*: includes full-drive encryption with BitLocker
    - *Home*: does not support BitLocker; may offer basic Device Encryption on compatible hardware
  - **Windows Information Protection (WIP)**
    - *Pro*: supports WIP to protect enterprise data and prevent leaks
    - *Home*: not available
  - **Group Policy Editor**
    - *Pro*: allows admin-level control over user and system settings (gpedit.msc)
    - *Home*: not included
  - **Remote Desktop Hosting**
    - *Pro*: can host Remote Desktop sessions (RDP)
    - *Home*: can only connect to other hosts, not be accessed remotely
  - **Hyper-V (Virtualization)**
    - *Pro*: supports Hyper-V for running virtual machines
    - *Home*: not available
  - **Enterprise Features**
    - *Pro*: supports tools like Assigned Access, Dynamic Provisioning, and Windows Update for Business
    - *Home*: lacks enterprise-level management tools

## File System

- **NTFS(New Technology File System)**
  - file system used in modern Windows
  - a journaling file system - automatically repairs folder/files using info stored in log
  - allows encryption (**EFS(Encryption File System )**)
  - permissions
    > full control - r, w, changing, delete
    > modify - r, w, delete
    > read & execute - r, execute
    > list folder contents - viewing content list, executing
    > read - r
    > write - w
  - **ADS (Alternate Data Streams)**
    - file attribute specific to NTFS
    - every file has at least 1 data stream `$DATA` and ADS allows more than one
    - explorer doesn't display ADS to user
    - malware writers use ADS to hide data

- system environment variable for Windows is `%windir%`.

## Features

- **BitLocker**
  - full disk encryption feature built into Windows (available on **Windows Pro**, **Enterprise**, and **Education** editions)
  - protects data by encrypting entire drives
  - prevents access if the device is lost or stolen
  - uses **TPM (Trusted Platform Module)** to securely store encryption keys
  - can also require a PIN or USB key for extra protection
  - supports both **OS drives** and **removable drives** (BitLocker To Go)
  - recoverable using a **BitLocker recovery key** (must be backed up when encryption is set up)

## User Accounts, Profiles, Permissions

- user accounts can be Administrator / Standard User

- **UAC (User Account Control)**
  - helps prevent malware from damaging PC
  - apps and tasks always run in the security context of a non-admin account unless admin authorizes
  - by default doesn't apply to built-in local admin account

## Windows Cmd

- `set`
  - `Path=` path
  
-`ver` determins version of OS
`systeminfo` lists OS info, system details, processor, memory
  - use `| more` to view line after line

- `ipconfig` shows network information (IP addr, subnet mask, default gateway)
  - `ipconfig /all` shows more

- `ping target_name` sends a ICMP packet and listens for response
- `tracert target_name` traces network route traversed to reach target
  - expects routers on the path to notify us if they drop a packet bc its TTL reaches 0
- `nslookup example.com` looks up a host/domain and returns its IP addr
  - `nslookup example.com 1.1.1.1` looks up the host using specified name server
- `netstat` displays current network connections & listening ports
  - `netstat -a` displays all established connections & listening ports
  - `netstat -b` shows the program associated with each listening port & established connection
  - `netstat -o` reveals PID associated with connection
  - `netstat -n` uses numerical form for addresses & port numbers

- `cd` equivalent to `pwd` in linux
  - but `cd target_dir` is the same; same with `cd ..`
- `dir` equivalent to `ls`
  - `dir /a` = `ls -a`
  - `dir /s` displayes files in current fir & all subdir
  - `tree` visually represents child dir & subdir
- `mkdir dir_name` makes directory
- `rmdir dir_name` deletes directory

- `type` dumps contents of file onto screen
  - `more` for longer files?
- `copy file destination_file` copies file to destination
  - `move` works the same
- `del` or `erase` deletes file

- `tasklist` lists running processes
  - `tasklist /FI "imagename eq sshd.exe"` sets filter image eq sshd.exe and searches for tasks related to sshd.exe
- `taskkill /PID target_pid` kills process with target_pid

- `chkdsk` checks the file system and disk volumes for errors and bad sectors
- `driverquery` displays list of installed device drivers
- `sfc /scannow` scans system files for corruption and repairs them if possible

- `shutdown /s` shuts down a system
- `shutdown /r` restarts a system
- `shutdown /a` aborts a scheduled shutdown

## PowerShell

- object-oriented - comparison to traditional cmd shell (text-based)
- commands are known as **cmdlets**
  - verb-noun naming convention
  - `Cmdlet -Property arg`
- **Piping** allows the output of one command be the input for another
  - more powerful in PS because it passes objects instead of text only
- display all properties by appending `| Format-List *`
- operators
  > `-eq` equals
  > `-ne` not equal
  > `-gt` greater than
  > `-ge` greater than or equal to
  > `-lt` less than
  > `-le` less than or equal to

- `Get-Command`
  - lists all available cmdlets, functions, aliases, and scripts that can be executed in current PS session
  - `Get-Command -CommandType "Function"` displays only type "Function"
- `Get-Help [command]`
  - provides usage, param, and examples
  - `Get-Help [command] -examples` outputs examples
- `Get-Alias`
  - lists all aliases available
  - Alias: alternative names for cmdlets
- `Find-Module`
  - searches for modules in online repos
  - `Find-Module -Name "pattern*"` searches for ones with a similar name(pattern) - `*` is a wildcard

- `New-Item -Path ".\path" -ItemType "Directory"`
  - creates new item at path
- `Remove-Item -Path ".\path"`
  - removes item at path
- `Copy-Item -Path .\path -Destination .\path`
- `Get-ChildItem -Path ".\path"`
  - alias of `ls`
- `Get-Content -Path ".\path"`
  - displays content

### Filtering Cmdlets

- `Where-Object -Property "Extension" -eq ".txt"`
  - filters all objects of .txt ext
  - other properties: e.g. `"Name"` 
- `Sort-Object -Propety property -descending`
  - sorts object by property in descending order
- `Select-Object property, property`
  - refines output to show only properties (columns)specified
  - `Select-Object -First 1` displays the first object
- `Select-String -Path ".\path" -Pattern "pattern"`
  - searches for text patterns within files
  - supports regex

- `Get-ComputerInfo`
  - retrievs system information
  - OS, hardware, BIOS, etc.
- `Get-LocalUser`
  - lists all local user accounts on the system
- `Get-NetIPConfiguration`
  - info about network interfaces
  - IP addr, DNS, gateway configurations
  - `Get-NetIPAddress` shows details for all IP addresses configured, including inactive ones

- `Get-Process`
  - provides detailed view of all currently running processes
- `Get-Service`
  - information about status of services on the machine
  - *for troubleshooting by system admin & forensics analysts*
- `Get-NetTCPConnection`
  - displays current TCP connections
  - *handy during incident response / malware analysis task*
- `Get-FileHash -Path .\path`
  - generates file hashes
  - *valuable in incident response, threat hunting, & malware analysis*

- `Invoke-Command`
  - runs commands on local and remote computers