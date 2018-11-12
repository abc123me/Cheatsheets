# Command formatting
`command_name <arguments>` Eg. `ls -l -a`
# Linux 101
`cat` - Reads a file<br>
`ls` - Lists all files in the current directory, similar to DOS's `DIR` command<br>
  - `-l` Makes the output detailed and `-a` Lists hidden files<br>
`cd` - Goes into a directory<br>
`touch` - Creates/Updates a file<br>
`vi` - Fancy ass (but overly complicated) file editor<br>
`nano` - Simple, good, easy-to-use file editor<br>
`grep` - Searches for a pattern<br>
`pwd` - Prints your current working directory

# Basic system administration
`top/htop` - Views information about running processes, `htop` is formatted<br>
`ifconfig` - Views all active network interfaces, use the -a argument to show hidden interfaces<br>
`iwconfig` - Views the wireless status of all wifi-enabled interfaces<br>
`lsusb/lspci` - Lists all devices on the usb/pci bus

# Package management
`apt/apt-get <mode>` - Most common package manager
- `install` installs a package
- `remove` removes a package
- `update` - Updates all packages
- `upgrade` - Upgrades the current linux kernel
- `purge` - Removes a package AND its configuration files
- `autoremove` - Removes all unused packages
