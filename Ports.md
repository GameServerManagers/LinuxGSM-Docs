## Generalities
 
* Port listening happens on a server
* Port redirection happens on a router
* Port opening happens on a firewall
* ip variable or host ip always needs to be a server's interface IP.

## View current settings

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

Every single game server has to be the only one using any of these ports.


## Changing default ports

Default ports set in the start parameters or game config. To alter them, which you need to do if want to run multiple servers, you will need to edit the main script file using vi or nano.  

```nano gameserver```

Example: for source games, you need to alter the following : 
````bash
# Start Variables
port="27015"
sourcetvport="27020"
clientport="27005"
ip="0.0.0.0"
````

**Reminder**: If you're running several servers, make sure you're using different ports on all of your servers.

**If there are no port settings** in your gameserver script, it means that you need to alter the config file to change them. The required file location will usually be displayed running `./gameserver details`.

**Home servers**: If your server is on a local network, you will need to make port redirections only for internet access.
The "ip" setting always needs to be set to the a server's interface IP, one that you see with ifconfig. Usually something like 192.168.x.x. So if it's a home server, don't put your public IP address here, put your local IP instead, or just leave `0.0.0.0` if you're unsure.

### Protip for running many servers

You probably want to make a table of your servers and ports in use in an excel or txt file.  
You probably will prefer a different port organization than the default one in order to make more servers more easily in a given port range.

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
If not, then your server doesn't start or listen properly. Check that you're trying to listen to an actual interface IP, check that ports are not already in use by something else, check that your server don't crash  upon start, check your console logs, try starting your server with `./gameserver debug`

2) **Check the firewall**  
[[Firewalls]] are source of many errors. When diagnosing stuff, disabling any firewall might help.

3) **Check port redirection** (local network only)  
Make sure that your router properly redirects the right ports displayed with `./gameserver details` with the right type (tcp and/or udp) to the right local IP. 