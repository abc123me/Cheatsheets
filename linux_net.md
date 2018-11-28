# ifconfig
Ifconfig is the universal interface (if) configuration (config) tool which allows very powerful control over the network interfaces on the computer
## Networking interfaces
Networking interfaces are practically any device that allows your computer to talk to another computer, there are an extremely wide variety of network interfaces such as ethernet, wireless or more uncommonly bridges, tunnels, loopbacks, etc. All linux distributions come with a default local loopback interface known as `lo`, this interface will always have an IP address of `127.0.0.1` or `localhost`. All network traffic heading to it is routed to the local host (hence the name) aka. your computer. Why is this useful? Well lets say you're testing you're new website on a local webserver and you want to access it from your current computer. Rather then entering your computers IP you can just provide `localhost` and it will automatically redirect to your computer. Heres an example of that in action:<br>
```
# The server: 
jeremiah@linux-pc:~$ echo "Hello, client!" | nc -l 1234

# The client:
jeremiah@linux-pc:~$ nc localhost 1234
Hello, client!

# The server (after typing "hello server"):
jeremiah@linux-pc:~$ echo "Hello, client!" | nc -l 1234
hello server
```
