# details

The `details` command allows access various useful information about the game server. Details are gathered from configs, parameters and server queries.

## Commands

### details

Standard: `./gameserver details`

Short: `./gameserver dt`

### post-details

`post-details` \(using hastebin\) is used to share server details, to help with support, while hiding sensitive information:

Standard: `./gameserver postdetails`

Short: `./gameserver pd`

## Details Provided

Various relevant details are provided including:

* Distro Details
* Performance
* Disk usage
* Server Name
* Server IP
* Server Ports
* Passwords
* Config File
* Backups
* Server parameters

## Example output

```text
Distro Details
===============================================================================================================================================================================================================
Distro:    Ubuntu 18.04.1 LTS
Arch:      x86_64
Kernel:    4.15.0-38-generic
Hostname:  arkserver.linuxgsm.com
tmux:      tmux 2.6
glibc:     2.27

Performance
Uptime:    24d, 16h, 17m
Avg Load:  0.20, 0.10, 0.09

CPU Model:      Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz
CPU Cores:      2
CPU Frequency:  2499.998 MHz

Mem:       total  used   free   cached  available
Physical:  3.9GB  2.1GB  1.6GB  1.5GB   1.6GB
Swap:      512MB  780KB  512MB

Storage
===============================================================================================================================================================================================================
Filesystem:      /dev/sda
Total:           79G
Used:            61G
Available:       14G
LinuxGSM Total:  7.9G
Serverfiles:     7.8G
Backups:         20K

ARK: Survival Evolved Server Details
===============================================================================================================================================================================================================
Server name:  LinuxGSM
Server IP:    1.2.3.4:7777
Maxplayers:   70
Default Map:  TheIsland
Status:       OFFLINE

arkserver Script Details
===============================================================================================================================================================================================================
Service name:           arkserver
arkserver version:      190106
User:                   lgsm
glibc required:         2.15
Discord alert:          off
Email alert:            off
Pushbullet alert:       off
IFTTT alert:            off
Mailgun (email) alert:  off
Pushover alert:         off
Telegram alert:         off
Update on start:        off
Location:               /home/arkserver
Config file:            /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini

Backups
===============================================================================================================================================================================================================
No Backups created

Command-line Parameters
===============================================================================================================================================================================================================
./ShooterGameServer "TheIsland?AltSaveDirectoryName=TheIsland?listen?MultiHome=1.2.3.4?MaxPlayers=70?QueryPort=27015?RCONPort=27020?Port=7777 -automanagedmods"

Ports
===============================================================================================================================================================================================================
Change ports by editing the parameters in:
/home/lgsm/arkserver/lgsm/config-lgsm/arkserver

Useful port diagnostic command:
netstat -atunp | grep ShooterGame

DESCRIPTION  DIRECTION  PORT   PROTOCOL
> Game       INBOUND    7777   udp
> RAW        INBOUND    7778   udp
> Query      INBOUND    27015  udp
> RCON       INBOUND    27020  tcp

Status: OFFLINE
```

