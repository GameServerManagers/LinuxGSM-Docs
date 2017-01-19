Game servers have many different ways of managing settings. Some are set within [[Start-Parameters]], inside the management script itself, while some are set within a configuration file.  
One of the goals of LGSM is to sort it out for you as much as possible, by providing all important settings out of the box, wherever they are.  
LGSM also usually provides a custom and more convenient configuration file.

## Getting information about config file

Assuming your script is called "gameserver", then the details command will provide you with config file information.

`./gameserver details`

Example:
````
./gmodserver details

Sample output:
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

## Config file naming

Whenever possible, LGSM uses a custom name for configuration files that contains the "${servicename}" variable in it in order to allow for running [[Multiple Servers]] with different config files. If the game doesn't allow for that, then the usual name will be used. For example, if you're running a `csgoserver`, then the default LGSM's `${servicename}` is `csgo-server` and the config file will be named `${servicename}.cfg` which gives `csgo-server.cfg`.

## Missing configuration file.

If LGSM provides a config file for a given server and detects it's been removed upon server start, it will now download it back.

## I found missing settings, what to do ?

If you found settings that are absent from the default configuration file provided by LGSM, or absent from start parameters and that would be useful to some people while not bothering others, then you can open an issue at https://github.com/GameServerManagers/LinuxGSM/issues