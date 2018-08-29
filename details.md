# Details

The `details` command allows you to access useful information about the game server.

## Commands

Standard: `./gameserver details`

Short: `./gameserver dt`

To share your details on Hastebin, for support, while hiding sensitive information automatically:

Standard: `./gameserver postdetails`

Short: `./gameserver pd`

## Details provided

You will be given various details that are relevent to your game server. These include:

* Distro Details
* Performance
* Disk usage
* Server Name
* Server IP
* Server Ports
* Rcon Password
* Config File
* Backups
* WebAdmin Username
* WebAdmin Password
* Server parameters

## Example output

```text
Distro Details
===============================================================================================================================================================
Distro:    Debian 7.7
Arch:      x86_64
Kernel:    2.6.32-042stab102.9
Hostname:  vps86887.ovh.net
tmux:      tmux 1.6
GLIBC:     2.13

Performance
===============================================================================================================================================================
Uptime:    0d, 17h, 36m
Avg Load:  0.00, 0.02, 0.00

Mem:       total   used   free
Physical:  1.0G    1.0G   17M
Swap:      128M    25M    102M

Disk Usage
===============================================================================================================================================================
Disk available:  5.4G
Serverfiles:     1.6G
Backups:         4.8M

Fistful of Frags Server Details
===============================================================================================================================================================
Server name:  Fistful of Frags Server
Server IP:    192.168.1.1:27015
RCON password:  rconpassword
Status:       OFFLINE

Service name:  fof-server
User:          fofserver
Location:      /home/fofserver
Config file:   /home/fofserver/serverfiles/fof/cfg/fof-server.cfg

Backups
===============================================================================================================================================================
No. of backups:    1
Latest backup:
    date:          Fri Jan 23 15:54:52 CET 2015
    file:          /home/fofserver/backups/fof-server-2015-01-23-155447.tar.gz
    size:          4.8M

Command-line Parameters
===============================================================================================================================================================
./srcds_run -game fof -strictportbind -ip 192.168.1.1 -port 27015 +clientport 27005 +tv_port 27020 +map fof_depot +servercfgfile fof-server.cfg -maxplayers 16

Ports
===============================================================================================================================================================
Change ports by editing the command-line
parameters in ./fofserver.

Useful port diagnostic command:
netstat -atunp | grep srcds_linux

DESCRIPTION  DIRECTION  PORT   PROTOCOL
> Game/RCON  INBOUND    27015  tcp/udp
```

