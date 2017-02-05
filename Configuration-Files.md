LinuxGSM makes config management easier in many different ways. However, some knowledge about it might be necessary.

# Config file's location
The "details" command will provide you some config files information.

### Command
`./gameserver details`

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
Location:            /home/gmodserver
Config file:         /home/gmodserver/serverfiles/garrysmod/cfg/gmod-server.cfg
````

# LinuxGSM custom config files
Whenever possible, LinuxGSM provides basic easy to use configuration files.  
A dedicated repository has been made so all server admins can benefit, even Windows admins.  
> https://github.com/GameServerManagers/Game-Server-Configs

This configuration file is automatically downloaded upon server installation.

# Config file naming
Whenever possible, LinuxGSM uses a custom name for configuration files that contains the "${servicename}" variable in it in order to allow the running of [[Multiple Servers]] with different config files. If the game does not allow for that, then the usual name will be used. In any case, `./gameserver details` will provide you with the config file's exact location.

### Example
For source servers, server.cfg is not used with LinuxGSM.

If you're running a `csgoserver`, then the default LinuxGSM `${servicename}` is `csgo-server` and the config file will be named `${servicename}.cfg` which gives `csgo-server.cfg`.

# Missing configuration file handling
LinuxGSM will always check a config file is present when starting a server.  
If a config file is missing, it will be simply re-download the default one.

# Where are the settings I'm looking for?
Game servers have many different ways of managing settings. Some are set within [[Start-Parameters]], inside the management script itself, while some are set within a configuration file.
 
One of the goals of LinuxGSM is to make managing these as easy as possible, by providing all important settings out of the box, wherever they are. There is no general rule about where config files are set. For that matter, you should always edit your `gameserver` script first in order to see available settings, then edit your configuration file.  
It is also a good idea to look for the official documentation of the game server that you're trying to run in order to find relevant information about settings.

### I found missing settings or an error with config files?
If you found settings that are absent from the default configuration file provided by LinuxGSM that would be a useful addition, then you can open an issue or a pull request. 
https://github.com/GameServerManagers/Game-Server-Configs