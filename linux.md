# Command formatting
`command_name <arguments>` Eg. `ls -l -a`<br>
`cmd >> file` - Appends command output to file<br>
`cmd > file` - Writes command output to file (destroying its old contents)<br>
`cmd1 | cmd2` - Readirects output of `cmd1` to `cmd2`
# Linux 101
`cat` - Reads a file<br>
`ls` - Lists all files in the current directory, similar to DOS's `DIR` command
 - `-l` Makes the output detailed
 - `-a` Lists hidden files
 - `-R` List files in subdirectories too (as well as their subdirectories)
 
`cd` - Goes into a directory<br>
`touch` - Creates/Updates a file<br>
`vi` - Fancy ass (but overly complicated) file editor<br>
`nano` - Simple, good, easy-to-use file editor<br>
`grep` - Searches for a pattern<br>
`find` - Lists all files in the directory and subdirectories, same as `ls -Rla` but faster
- A directory can be provided to filter the search
- Lets say you need to find your DHCP configuration file, you can use `find /etc | grep dhcp`

`pwd` - Prints your current working directory<br>
`sudo` - Gives you the privledges of another user, default root
- The username of the other user is specified with the `-u <user>` argument
- Only certain users are allowed to use the `sudo` command, these users are the users specified by the `/etc/sudoers` file

# Basic system administration
`top/htop` - Views information about running processes, `htop` is formatted<br>
`ifconfig` - Views all active network interfaces, use the -a argument to show hidden interfaces<br>
`iwconfig` - Views the wireless status of all wifi-enabled interfaces<br>
`dhclient <iface>` - Configures DHCP for a specified interface<br>
`lsusb/lspci` - Lists all devices on the usb/pci bus

# Package management
`apt/apt-get <mode>` - Most common package manager
- `install` installs a package
- `remove` removes a package
- `update` - Updates all packages
- `upgrade` - Upgrades the current linux kernel
- `purge` - Removes a package AND its configuration files
- `autoremove` - Removes all unused packages
