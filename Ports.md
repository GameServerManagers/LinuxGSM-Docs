# Generalities
 
* Port listening happens on a server.
* Port redirection happens on a router.
* Port opening happens on a firewall.
* The IP variable `ip=` always needs to be the server interface IP, not your routers external IP.
* Each game server instance has to have its own unique ports, this means they cannot share ports.

# View current settings

To view your current server ports, input: 

`./gameserver details`

Example output sample:

````
Useful port diagnostic command:
netstat -atunp | grep srcds_linux

DESCRIPTION  DIRECTION  PORT   PROTOCOL
> Game/RCON  INBOUND    27027  tcp/udp
> SourceTV   INBOUND    27052  udp
< Client     OUTBOUND   27002  udp
````

# Changing default ports

Default ports are set in either the start parameters or game config. 
You can use `./gameserver details` to find out where to edit port settings

	# Ports
	# =====================================
	# Change ports by editing the parameters in:
	# /home/lgsm/qlserver/serverfiles/baseq3/ql-server.cfg

To alter them you will need to edit the file using `nano`.

Example: for source games, you need to alter the following: 
````bash
# Start Variables
port="27015"
sourcetvport="27020"
clientport="27005"
ip="0.0.0.0"
````

## What ports can be used?

You can use any port you like as long as it is not already in use. It is up to you how to setup your own port allocation. It is recommended that you keep your ports close together and sequential i.e 27016,27016,17017 to save confusion. Some servers ports by default are not sequential, however there is nothing stopping an admin from changing this. Example for source servers; you could set the port 27015, sourcetv port 27016, client port 27018. The next game server instance could simply follow on from this.

>Reminder: If you're running several servers, make sure you're using different ports on all of your servers.

# Multiple IP addresses
If your server has multiple dedicated IP address allocated to your server it is possible for game servers to have the same ports but binded to the different IP addresses. You will need to set the specific ip address you want to use in the LinuxGSM or game config.

# Home Servers
Home servers are a great way to experiment with game servers or can be used as a permanent option if you have the bandwidth. There are extra steps required on your home router to allow external access to your game server. This will normally involve opening ports on the router firewall and/or port forwarding. See your routers manual for specific instructions.

https://www.howtogeek.com/66214/how-to-forward-ports-on-your-router/


## ip= setting for home servers
If your server has multiple interfaces you will be promoted to specify the server IP you want to use.

You will need to set the IP address of the servers LAN interface (e.g 192.168.1.2), not your routers external IP. Setting this incorrectly will prevent the game server ports from binding and your server will not start.

# Track your ports
If you are running several game servers it is a good idea to create a spreadsheet of the ports you have used. Allowing you to keep track of what you have already used.

### Ideas to set ports for multiple source servers

For example for source games, a common practice is to use ports in the 270xx range. Other values may work too.

**Method 1**

A good idea to be close the the steam standard but keep it simple, and be able to make 25 servers per hundred range, is to start with the first server that way : 

````bash
port="27025"
sourcetvport="27050"
clientport="27000"
````

Then increment those port  by 1 for every new server. 25 servers are using 75 ports. After making 25 servers, if you need more, or if you want to separate servers, a good idea is to ad +100 to this 27000 range. Example: 

````bash
port="27125"
sourcetvport="27150"
clientport="27100"
````

**Method 2**

You can use ports next to each other, like that : 

    port="27001"
    sourcetvport="27002"
    clientport="27000"

Some people find it more convenient. You'll be able to make more servers per hundred of ports that way (around 33 instead of 25), but, this is a non-standard way. 

**Method 3** 

You can get new IPs for your dedicated server, and assign some servers to different IPs.

## Diagnosing server accessibility

1) **Make sure your server is listening properly**  
Before anything else, you need to know if your sever is actually listening.
Input : `./gameserver details` and look for this kind of diagnose command:
````
Useful port diagnostic command:
netstat -atunp | grep srcds_linux
````
Run it, and see if your server is actually listening.
If not, then your server has not started or not listen properly. Check that you are trying to listen to an actual interface IP, check that ports are not already in use by something else, check that your server don't crash upon start, check your console logs, try starting your server with `./gameserver debug`

2) **Check the firewall**  
[[Firewalls]] are source of many errors. When diagnosing issues temporarily disabling any firewall might help.

3) **Check port forwarding** (local network only)  
Make sure that your router properly redirects the right ports displayed with `./gameserver details` with the right type (tcp and/or udp) to the right local IP. 