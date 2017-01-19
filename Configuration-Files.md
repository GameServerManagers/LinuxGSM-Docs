LGSM makes config management easier in many different ways. However, some knowledge about it might be necessary.

# Config file's location

The "details" command will provide you some config files information.

### Command
`./gameserver details`

Note: Replace "gameserver" with your actual script name.

### Sample output example
````
./gmodserver details

gmodserver Script Details
==================================================================================
Service name:        gmod-server
gmodserver version:  170110
User:                ultimatebyte
GLIBC required:      2.15
Email alert:         off
Pushbullet alert:    off
Update on start:     off
Location:            /home/ultimatebyte
Config file:         /home/ultimatebyte/serverfiles/garrysmod/cfg/gmod-server.cfg
````

# LGSM custom config files

Whenever possible, LGSM provides custom and more convenient configuration files.  
A dedicated repository has been made for that matter so that any user, even Windows ones can benefit from it.  
https://github.com/GameServerManagers/Game-Server-Configs  
This configuration file is automatically downloaded upon server installation.

# Config file naming

Whenever possible, LGSM uses a custom name for configuration files that contains the "${servicename}" variable in it in order to allow for running [[Multiple Servers]] with different config files. If the game doesn't allow for that, then the usual name will be used. In any case, `./gameserver details` will provide you with the config file's exact location.

### Example
For source servers, server.cfg is no longer used when using LGSM.

For example, if you're running a `csgoserver`, then the default LGSM's `${servicename}` is `csgo-server` and the config file will be named `${servicename}.cfg` which gives `csgo-server.cfg`.

# Missing configuration file handling

When LGSM provides a config file for a server, it will check if the file exists upon server start.  
If it doesn't, it will be downloaded back.

# Where are the settings I'm looking for?

Game servers have many different ways of managing settings. Some are set within [[Start-Parameters]], inside the management script itself, while some are set within a configuration file.  
One of the goals of LGSM is to sort it out for you as much as possible, by providing all important settings out of the box, wherever they are. 
There is no general rule about where config files are set. For that matter, you should always edit your `gameserver` script first in order to see available settings, then edit your configuration file.  
It is also a good idea to look for the official documentation of the game server that you're trying to run in order to find relevant information about settings.

### I found missing settings, what to do ?

If you found settings that are absent from the default configuration file provided by LGSM, or absent from start parameters and that would be useful to some people while not bothering others, then you can open an issue at https://github.com/GameServerManagers/LinuxGSM/issues