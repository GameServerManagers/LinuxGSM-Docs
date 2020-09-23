# Ports

You will need to give attention to ports in multiple cases.

Here are the most common ones:

* When you want to run [Multiple Game Servers](../features/multiple-game-servers.md) on the same machine
* When you have a strict firewall and you need to open the right ports in order to let people connect to your server \(see [Firewalls](../linux/firewalls.md)\)
* When you need to forward ports on a NAT to the desired local IP in order for your server to be reachable from outside the local network \(likely from the internet\)

## Vocabulary

* `Port listening` is what a service like a game server does in order to receive packets from incoming connections: by listening to a port, the program waiting for incoming packets on a given port.
* `Port redirection` happens on a router, in the NAT part: it consists in forwarding incoming traffic on a given port to a specific local \(regarding the router\) IP.
* `Port opening` happens on a firewall, it consists of allowing traffic to a port.
* The IP variable `ip=` always needs to be the server interface IP, not your routers external IP: a service on a server can only listen on a local IP that is present on an interface of the hosting machine.
* In order to `run multiple game servers` on the same machine, you need to make sure they all use different ports, or if your server has multiple public IPs, that they are bound to different IPs.

## Setting ports

Listening ports are usually set within your start parameters or game server config file.

For info about start parameters, see [Start Parameters](start-parameters.md) and [LinuxGSM Config](linuxgsm-config.md) For info about your game server config, see [Game Server Config](game-server-config.md).

## View current settings

To view your current server ports, input:

`./gameserver details`

Example output sample:

```text
Useful port diagnostic command:
netstat -atunp | grep srcds_linux

DESCRIPTION  DIRECTION  PORT   PROTOCOL
> Game/RCON  INBOUND    27027  tcp/udp
> SourceTV   INBOUND    27052  udp
< Client     OUTBOUND   27002  udp
```

## Changing default ports

Default ports are set in either the [start parameters](start-parameters.md) or [game config](game-server-config.md). You can use `./gameserver details` to find out where to edit port settings

```text
# Ports
# =====================================
# Change ports by editing the parameters in:
# /home/lgsm/qlserver/serverfiles/baseq3/ql-server.cfg
```

To alter them you will need to edit the file using `nano`.

Example: for source games, you need to alter the following:

```bash
# Start Variables
port="27015"
sourcetvport="27020"
clientport="27005"
ip="0.0.0.0"
```

### Which ports can be used?

You can use any port as long as it is not already in use and it is up to you to set up port allocation. It is recommended that ports are close together and sequential i.e 27015, 27016, 27017 to save confusion. Some servers ports by default are not sequential, however, there is nothing stopping you from changing this. Example for source engine game servers; you could set the port 27015, source tv port 27016, client port 27018. The next game server instance could simply follow on from this.

{% hint style="info" %}
If you're running multiple game servers, make sure you're using different ports on all of your game servers to avoid a port conflict.
{% endhint %}

## Multiple IP addresses

Should a server have multiple dedicated IP addresses allocated, it is possible for game servers to have the same ports but bound to the different IP addresses. Admins will need to set the specific IP address in the LinuxGSM config or game config.

## Home Servers

Home servers are a great way to experiment with game servers, for LAN partys or can be used as a permanent option if you have the bandwidth. There are extra steps required on your home router to allow external access to your game server. This will normally involve opening ports on the router firewall and/or port forwarding. See [this link](https://www.howtogeek.com/66214/how-to-forward-ports-on-your-router/) for basic instructions. See your router's manual for specific instructions.

### Specifying you IP for Home Server

If you want to specify the game server IP address using the `ip=` you will need to set the IP address of the servers LAN interface \(e.g 192.168.1.2\), not your routers external IP. Setting this incorrectly will prevent the game server ports from binding and your server will not start.

## Port Allocation Scheme

Each type of server has a default set of ports. This is fine to use if only one server is being set up. However, if multiple servers are being used a port scheme needs to be considered. There is no requirement to stick to specific ports but it is recommended they are in a logical order.

Source Default Ports

```text
port="27015"
sourcetvport="27020"
clientport="27005"
```

### Incremental \(recommended\)

You can allocate ports incrementally, one after the other. With each server following on from the last.

```text
port="27015"
sourcetvport="27016"
clientport="27017"
```

This scheme is the simplest option to avoid confusion when managing ports. Plus this is the most efficient scheme reducing unused ports.

### Standard Port Increment

This method increments each type of port keeping the scheme closer to the default. It is not as efficient but keeps ports more "standard".

```bash
port="27016"
sourcetvport="27021"
clientport="27006"
```

Then increment those port by 1 for every new server. 25 servers are using 75 ports. After making 25 servers, if you need more it is a good idea is to add +100 to this 27000 range.

```bash
port="27125"
sourcetvport="27150"
clientport="27100"
```

### Separate IP Addresses

You can get new IP addresses for your dedicated server, and assign each server a new IP. This scheme is quite inefficient.

## Track your ports

If you are running several game servers it is a good idea to create a spreadsheet of the ports you have used. Allowing you to keep track of what you have already used.

## Diagnosing server accessibility

### Check port are bound

Ensure the game server ports are bound and listening before anything else, you need to know if your server is actually listening. Input : `./gameserver details` and look for this kind of diagnose command:

```text
Useful port diagnostic command:
netstat -atunp | grep srcds_linux
```

Running the command will bring up any ports that are listening. If not, the game server has not started or not correctly binding to its allocated ports. 

* Check that ports are not already in use by something else.
* Check that you are trying to listen to an actual interface IP.
* Check that ports are not already in use by another application.
* check that the server does not crash upon start by checking console logs or try starting the server with `./gameserver debug`

### Check the Firewall

[Firewalls](../linux/firewalls.md) are a regular source of connectivity issues. When diagnosing connection issues temporarily disabling a firewall will help identify if it is the source of the problem.

### Check Port Forwarding \(Local Networks\)

Ensure that the router correctly redirects incoming traffic to the correct ports and local IP displayed with `./gameserver details` with the correct protocol \(TCP and/or UDP\).

