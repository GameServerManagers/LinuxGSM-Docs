# Trackmania Nations Forever / Trackmania United Forever
![TMNF Logo](https://www.gamers.org/tmf/banner.jpg)

## Ports

- Game Port Default: 2350 UDP
- XMLRPC Port: 5000 TCP

## Online Hosting Requirements

Hosting an Internet accessable Online Server requieres a login to the master server. It can't be your game login and every server needs an unique account. 

For LAN Hosting a server login isn't required!

### Trackmania Nations Forever Server Account

- Start your gameclient and create an account there

### Trackmania United Forever Server Account

- Login with your gaming credentials at http://official.trackmania.com/tmf-playerpage/ (either use http or setup your browser to support older https protocols)
- On "Dedicated servers" you have to type your Serial Code of the Game to allow access of dedicated server accounts. If your bought Trackmania United Forever on Steam it's easy to get your product code
- Create there a new login for the dedicated Server

## Startparameters

| Startparameter | Function
|--|--|
| dedicated_cfg=xxx | Specifies the name of the dedicated configuration |
| game_settings=xxx | Specifies the name of game settings configuration |
| login=xxx | Username of Server Account |
| password=xxx | Password of Server Account |
| servername=xxx  | Name of the Server |
| serverpassword=xxx | Connection Password for clients to connect if you want to make the server private |
| lan | Start server in LAN mode |
| forceip=xxx(:xx) | Forces the public ip address (and optionally port) to this value |
| bindip=xxx(:xx) | Binds server to ip address if multiple network interfaces are on the machine |
| join=xxx | Joins a server, to make a relay server. (xxx = the server ip adress with optional port, or the server login) |
| joinpassword=xxx | Password to use to join the remote server if the server is private |
| loadcache | Loads the "checksum.txt" instead of recomputing it, to speed up first launch time if P2P is enabled. *DO NOT USE* if you run several servers in the same directory |
| nologs | Disables the creation of "GameLog.txt" and "ConsoleLog.txt" in Logs/ directory |
| noautoquit | Keeps the server running "waiting for rpc commands", even if it is not live (with a map loaded and ready to receive players) |
| nodaemon | Doesn't detach the process |
| verbose_rpc_full | Display the whole contents of the xml-rpc requests the dedicated server receives. |
| verbose_rpc | Displays the xml-rpc requests the dedicated server receives, but only the name of the XmlRpc? command and some parameters |

Example: `TrackmaniaServer /dedicated_cfg=dedicated_cfg.txt /game_settings=MatchSettings/custom_game_settings.txt /nodaemon /lan`

Source of parameters: https://web.archive.org/web/20221003213817/https://www.tm-forum.com/viewtopic.php?p=154464#p154464

## Configuration

Configuration happens on two `.txt` files which are formatted in XML, name can be anything you like. The dedicated configuration needs to be located in `GameData/Config/` and game settings in `GameData/Tracks/`. 

## Source

More Information about Serverhosting can be aquired on https://server.xaseco.org/