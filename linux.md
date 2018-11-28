# Linux 101 - Fundamentals
## Command formatting
- `command_name <arguments>`
- Commands are normally found in locations such as `/bin` and `/usr/bin`, determined by your `PATH` variable
- The `which` command will tell you the location of the command 
  - Eg. `which which` returns `/usr/bin/which`
  
## Piping
- `cmd >> file` - Appends command output to file
- `cmd > file` - Writes command output to file (destroying its old contents)
- `cmd 2> file` - Writes command errors to file (destroying its old contents)
- `cmd < file` - Reads file and uses it as input for cmd
- `cmd1 | cmd2` - Redirects output of `cmd1` to `cmd2`

## Special files/letters/directories
- `*` - Wildcard, substituted for a letter
  - Eg you have 4 files `aa ab ba bb`: `*` would be replaced by `aa ab ba bb` and `a*` would be replaced by `aa ab`
- `~` - Tilda, substituted for the current user's home directory
  - By default this is `/home/username`
- `$` - Variable, Allows you to read an environment variable
  - $PATH is the most common environment variable containing the locations of common programs such as `ls` located in `/bin/ls`
  - Some distros append `~/bin` to your `$PATH` so you can write programs in ~/bin and execute them as commands
- `\` - Escape character
  - If you write a space in the terminal normally it will interpret multiple arguments, to fix this we use the `\` character which allows typing special characters eg. `\ ` would make a space or `\\` would make a backslash

## Linux filesystem
- `/` - The root, everthing must be inside of `/`
- `/sys` - System devices, such as keyboard LED's etc.
- `/dev` - Block devices, these can be anything really
  - `/dev/sd*` - Normally hard drives
  - `/dev/tty*` - Terminals, these can also be found in the `/dev/pts/*` directory
- `/etc` - Configuration files, etc.
  - `/etc/network/interfaces` - Network interface configuration file
  - `/etc/rc.local` - Linux startup script, runs on startup
  - `/etc/fstab` - Declares all drives including the root partition (aka. `/`)
  - `/etc/default/grub` - GRUB Boot loader configuration file
- `/home` and `/root` - Home directories for different users
  - By default a normal user has a home folder at `/home/username`
  - However, root has its own special folder at `/root`
- `/lib` - Essential system libraries 
- `/bin` - Essential system binaries (aka. programs)
- `/usr` - User directory, anything belonging to a user goes here
  - `/usr/bin` - User installed binaries
  - `/usr/lib` - User installed libraries
- `/proc` - Process specific files
  - Whenever a process starts a folder is created here with is PID
  - `/proc/cpuinfo` contains information about the CPU
  - `/proc/stat` contains information about system resources such as CPU and Memory usage
- `/tmp` - Temporary files, deleted when system is rebooted
- `/var` - Logging and other system information
- `/opt` - Optional files and folders (rarely used)
- `/media` and `/mnt`
  - Normally used as places to mount drives, etc.
  - `/mnt` normally contains user specially mounted devices
  - `/media` normally contains media such as cd-roms, flashdrives, floppies, etc.

# Linux 101 - Commands
## Directory navigation
- `cd` - Goes into a directory<br>
- `ls` - Lists all files in the current directory, similar to DOS's `DIR` command
  - `-l` Makes the output detailed
  - `-a` Lists hidden files
  - `-R` List files in subdirectories too (as well as their subdirectories)
  - `pwd` - Prints your current working directory<br>
- `mkdir <name>` - Makes a directory
## File modification
- `cat` - Reads a file<br>
- `touch` - Creates/Updates a file<br>
- `vi` - Fancy ass (but overly complicated) file editor<br>
- `nano` - Simple, good, easy-to-use file editor<br>
## Other useful stuff
- `tmux` - Termianl multiplexer, allows multiple terminals in one terminal
  - `Ctrl + B then [Arrow key]` moves to another terminal
  - `Ctrl + B then Ctrl + [Arrow keys]` resizes the current terminal
  - `Ctrl + B then %` creates a new terminal to the right of the old terminal
  - `Ctrl + B then "` creates a new terminal under the old terminal
  - `Ctrl + B then x` force kill the current terminal
  - `Ctrl + B then d` Detach so you can access it again with `tmux attach` after logout
- `grep` - Searches for a pattern
  - Lets say you forgot where your `hello.conf` file is
  - `find / | grep hello.conf` will show you all files in your computer that contains `hello.conf` in their filenames
- `find` - Recursively lists all files (not directories)
  - A directory can be provided to filter the search
  - Lets say you need to find your DHCP configuration file, you can use `find /etc | grep dhcp`
- `sudo` - Gives you the privledges of another user, default root
  - The username of the other user is specified with the `-u <user>` argument
  - Only certain users are allowed to use the `sudo` command, these users are the users specified by the `/etc/sudoers` file


# Linux 101 - Basic system administration
## Resource monitoring
- `top` - Views information about running processes and system resources
- `htop` - A formatted version of `top` (it also has color and custom themes)
- `cat /proc/stat` - Raw CPU time data, useful for scripts
## Hardware monitoring
- `lsusb/lspci` - Lists all devices on the usb/pci bus
- `lshw` - Lists all hardware attached to the computer
  - The `-C <name>` option can be used to list all items of a specific class
  - Eg. `lshw -C Memory` lists all memory in the computer
- `lscpu` - Lists info about the current CPU(s) installed
## Kernel modules / Drivers
- `lsmod` - Lists all currently loaded kernel modules
- `modprobe` - General tool for managing kernel modules
- `insmod` - Insert a kernel module
- `rmmod` - Remove a kernel module
## Networking
- `ifconfig` - Views all active network interfaces, use the -a argument to show hidden interfaces
  - `ifconfig <iface> <ip>` - Changes the IP of `<iface>` to `<ip>`
- `iwconfig` - Views the wireless status of all wifi-enabled interfaces
- `iptables` - Modifies the kernel's routing tables
- `dhclient <iface>` - Configures DHCP for a specified interface
## Software stuff
- `uname` - Gets kernel info, add `-r` to get the kernel version
- `apt/apt-get <mode>` - Most common package manager
  - `install` installs a package
  - `remove` removes a package
  - `update` - Updates all packages
  - `upgrade` - Upgrades the current linux kernel
  - `purge` - Removes a package AND its configuration files
  - `autoremove` - Removes all unused packages
- `dmesg` - System logs, piping into `tail` can be useful
  - Eg. `dmesg | tail -n 5` tells you the last 5 things that happened, in my case 
  ```
    [887434.014362] bnx2 0000:05:00.0 enp5s0f0: NIC Copper Link is Up, 10 Mbps full duplex
    [887434.014394] , receive & transmit flow control ON
    [887434.014532] br0: port 3(enp5s0f0) entered forwarding state
    [887434.014571] br0: port 3(enp5s0f0) entered forwarding state
    [887449.052067] br0: port 3(enp5s0f0) entered forwarding state
  ```
- `journalctl` - More system logs
