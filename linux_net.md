# Networking interfaces
Networking interfaces are practically any device that allows your computer to talk to another computer, there are an extremely wide variety of network interfaces such as ethernet, wireless or more uncommonly bridges, tunnels, loopbacks, etc. 
## ifconfig
Ifconfig is the interface (if) configuration (config) tool which allows very powerful control over the network interfaces on the computer, and best of all it comes pre-installed with basically every linux distribution today! Ifconfig allows simple configuration such as setting IP address, netmask, etc. The basic syntax is as follows: `ifconfig IFACE IP_ADDRESS netmask NETMASK ETC`. In case your distribution don't come with ifconfig *cough* Ubuntu server 18.04 *cough* you can install it by installing the `ifupdown` package, `ifupdown` not only gives you access to `ifconfig` but other helpful commands like `ifup/ifdown` which is a convient shortcut to bring an interface up/down.
### /etc/network/interfaces
This is the configuration file for the `ifupdown` suite, it allows you to pernamentaly save your changes made by `ifconfig`. An example interfaces file is shown here:
```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug eth0
iface eth0 inet dhcp
```
The `auto` keyword makes an interface required for bootup, the `allow-hotplug` keyword does just what it says, allows hot plugging. `iface IFACE inet MODE` declares an interface `IFACE` with mode `MODE`, the mode can be DHCP, Static, or Manual. A manual interface will be configured by another program, while static interfaces have a static IP and dhcp interfaces are assigned an IP via. the DHCP autoconfiguration protocol. My personal routing server's interface file is shown below (hopefully demonstrating a more complex interfaces file so you can get the syntax down):
```
# The loopback network interface
auto lo
iface lo inet loopback

# Quad port gigabit ethernet controller
allow-hotplug enp4s0f0
iface enp4s0f0 inet manual
allow-hotplug enp4s0f1
iface enp4s0f1 inet manual
allow-hotplug enp5s0f0
iface enp5s0f0 inet manual
allow-hotplug enp5s0f1
iface enp5s0f1 inet manual

# Gigabit ethernet card
allow-hotplug enp6s0
iface enp6s0 inet manual

# Shitty motherboard 100Mb ethernet
allow-hotplug enp0s7
iface enp0s7 inet manual

# Ethernet bridge
auto br0
iface br0 inet static
	address 192.168.1.1
	netmask 255.255.255.0
	bridge-ports enp4s0f0 enp4s0f1
	bridge-ports enp5s0f0 enp5s0f1
	bridge-ports enp6s0
	bridge-ports enp0s7
```
### Local loopback
All linux distributions come with a default local loopback interface known as `lo`, this interface will always have an IP address of `127.0.0.1` or `localhost`. All network traffic heading to it is routed to the local host (hence the name) aka. your computer. Why is this useful? Well lets say you're testing you're new website on a local webserver and you want to access it from your current computer. Rather then entering your computers IP you can just provide `localhost` and it will automatically redirect to your computer. Heres an example of that in action:<br>
```
# The server: 
jeremiah@linux-pc:~$ echo "Hello, client!" | nc -l 1234

# The client:
jeremiah@linux-pc:~$ nc localhost 1234
Hello, client!

# The server (after typing "hello server" into the client):
jeremiah@linux-pc:~$ echo "Hello, client!" | nc -l 1234
hello server
```
As you can see in the example a network socket is created between the two processes even though they are on the same machine.
### Ethernet / WiFi
Depending on your linux distribution the naming scheme of interfaces can change but for WiFi and ethernet this is normally a result of the following formula `enp + VENDOR_ID + s + PORT_ID` so if you had a dual port ethernet card with a `VENDOR_ID` of 5 you would see `enp5s0` and `enp5s1` in `ifconfig`, Wireless is the same way but the `enp` is replaced with `wlp`. However do not rely on this naming scheme since it isn't the same for all devices and distributions. For example in debian ethernet cards are `eth0, eth1, ethN`, and wireless is `wlan0, wlan1, wlanN`.
### Bridges (from package `bridge-utils`)
Bridges allow you to connect multiple interfaces together to make one big network interface, using this you can create your own network switches, redundent connections, and multiple cable connections for faster speeds.
