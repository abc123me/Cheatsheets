# Command formatting
- `command_name <arguments>`
- Commands are normally found in locations such as `/bin` and `/usr/bin`, determined by your `PATH` variable
- The `which` command will tell you the location of the command 
  - Eg. `which which` returns `/usr/bin/which`
## Piping
- `cmd >> file` - Appends command output to file<br>
- `cmd > file` - Writes command output to file (destroying its old contents)<br>
- `cmd 2> file` - Writes command errors to file (destroying its old contents)<br>
- `cmd < file` - Reads file and uses it as input for cmd<br>
- `cmd1 | cmd2` - Redirects output of `cmd1` to `cmd2`<br>
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

# Linux filesystem
`/` - The root, everthing must be inside of `/`
`/sys` - System devices, such as keyboard LED's etc.
`/dev` - Block devices, these can be anything really
- `/dev/sd*`
# Linux 101
## Directory navigation
- `cd` - Goes into a directory<br>
- `ls` - Lists all files in the current directory, similar to DOS's `DIR` command
  - `-l` Makes the output detailed
  - `-a` Lists hidden files
  - `-R` List files in subdirectories too (as well as their subdirectories)
  - `pwd` - Prints your current working directory<br>
- `mkdir <name>` - Makes a directory
`cat` - Reads a file<br>

 
`touch` - Creates/Updates a file<br>
`vi` - Fancy ass (but overly complicated) file editor<br>
`nano` - Simple, good, easy-to-use file editor<br>
`grep` - Searches for a pattern<br>
`find` - Lists all files in the directory and subdirectories, same as `ls -Rla` but faster
- A directory can be provided to filter the search
- Lets say you need to find your DHCP configuration file, you can use `find /etc | grep dhcp`

`sudo` - Gives you the privledges of another user, default root
- The username of the other user is specified with the `-u <user>` argument
- Only certain users are allowed to use the `sudo` command, these users are the users specified by the `/etc/sudoers` file

# Basic system administration
`top/htop` - Views information about running processes, `htop` is formatted<br>
`ifconfig` - Views all active network interfaces, use the -a argument to show hidden interfaces<br>
`iwconfig` - Views the wireless status of all wifi-enabled interfaces<br>
`dhclient <iface>` - Configures DHCP for a specified interface<br>
`lsusb/lspci` - Lists all devices on the usb/pci bus<br>
`lsmod` - Lists all currently loaded kernel modules (aka. drivers)

# Package management
`apt/apt-get <mode>` - Most common package manager
- `install` installs a package
- `remove` removes a package
- `update` - Updates all packages
- `upgrade` - Upgrades the current linux kernel
- `purge` - Removes a package AND its configuration files
- `autoremove` - Removes all unused packages
