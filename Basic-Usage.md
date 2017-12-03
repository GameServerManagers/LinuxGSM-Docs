# Introduction
The basic usage of LinuxGSM to help with getting started.
For more advanced usage see pages for a specific command.

> Note: Generic "gameserver", "gamename" and "username" values are used for this guide; replace these with your own values.

# Installation

The full installation guide can be found at [gameservermanagers.com](https://gameservermanagers.com/)
Follow the basic instructions to install a game server.

# Available Commands

To see a list of available commands, execute `./gameserver` with no argument.

Example:
````bash
gameserver@game:~$ ./gameserver
Usage: ./gameserver [option]
GameName - Linux Game Server Manager - Version 170110
https://gameservermanagers.com/gameserver

Commands
start             st |Start the server.
stop              sp |Stop the server.
restart           r  |Restart the server.
...
````

A wiki page for every command is available. Basic tasks and commands are detailed below.

See [[Command List]] for a full list of commands.

# Running your Server

To [[start-stop-restart]] your server, use the following commands:

````bash
./gameserver start
./gameserver stop
./gameserver restart
````

# Getting Game Server and Hardware Information

The [[details]] command provides information relevant to the game server. Such as config file's location, start parameters settings, and many other information.

````bash
./gameserver details
````

# Configuring a Server
Configuring a game server requires altering settings in various locations. Configuration is split in two main sections, Linuxgsm configuration and Game configuration.

* LinuxGSM configuration handles settings related to LinuxGSM
* Game configuration handles settings related to the dedicated server.

## LinuxGSM Config
LinuxGSM configuration handles settings related to LinuxGSM and game server definitions. For example settings for alerts and backups. Definitions for game server name, location, Steam App ID, start parameters.

LinuxGSM Configs are located in 

```
lgsm/config-lgsm/gameserver
```

For more info see [[LinuxGSM Config Files]].

## Game Config
Game servers have several methods of configuration. This means configuration will vary depending upon which game server is being setup.

There are two main methods a game server is configured, either with config files or start parameters. Servers can use one or a mixture of these methods.

> note: LinuxGSM will also priorities the usage of config files over start parameters.

## Config Files

Most servers use a configuration file to alter settings.  
Whenever possible, LinuxGSM provides an enhanced default config file from https://github.com/GameServerManagers/Game-Server-Configs.

The [[details]] command will provide you with the config file location.

````bash
./gameserver details
````
Sample output: 
````
Config file:   /home/username/serverfiles/gamename/cfg/gamename-server.cfg
````
You can edit this file with any Linux text editor such as `nano` or `vi`.

LinuxGSM does not provide specific information about altering this configuration file except for some special games showed in "Game Info" section from the [wiki](https://github.com/GameServerManagers/LinuxGSM/wiki). There are many websites that provide documentation and support on configuring your server.

## Start Parameters

Many game servers require [[Start-Parameters]] when configuring some settings. Start parameters are command line options appended to server's executable when you start it.

These parameters can be reviewed using the [[details]] command.

To alter them, edit the LinuxGSM config files using `vi` or `nano` and edit variables from the `## Server Start Settings` section. The `#### LinuxGSM Settings ####` section allows customising many different settings.

# Updating your server

Most servers can be updated automatically using the update feature that uses SteamCMD.

## update command

The [[update]] command checks if an update is available for the server. The server will update and restart only if required.
````bash
./gameserver update
````

## validate command

For SteamCMD servers (available from Steam), the [[validate]] command checks the integrity from server files to make sure they exactly match the remote version. It can be useful if an update fails or if files get corrupted for some reason.

````bash
./gameserver validate
````

# Updating your LinuxGSM script
LinuxGSM has the ability to self [[update-functions]].

````bash
./gameserver update-functions
````

This will allow you to get various fixes and possibly new functionalities.  
In some rare cases, you will need to update your main "gameserver" script as well in order to enjoy all new functionalities.

# Automating tasks

You can use [[Cronjobs]] to automate any LinuxGSM function.
Most used ones are:
* Automatically check for updates [[update]]
* Automatically check for server crash and restart if needed [[monitor]]
* Automatically keep LinuxGSM up to date [[update-functions]]
* Automatically restart the server at a given time [[start-stop-restart]]
* Automatically update and restart the server [[force-update]]
* Automatically backup the server [[backup]]

For more details, see [[Cronjobs]]

## Running on Boot
To run a server [[On-Boot]], we advise to use a monitor cronjob: any server that was online before a machine reboot will be restarted. 

See [[On-Boot]] or [[Monitor#automated-monitoring]] for more information.

# Troubleshooting

## Logs

LinuxGSM and game console logs are available. They can help you checking for your server's health and diagnosing issues.

Logs location: `/home/username/log/`

## Console

The [[console]] command allows you to view the live console of a running server and to enter commands. When the game offers a good console output, it might help diagnosing issues along with logs.

````bash
./gameserver console
````

To exit the console press “CTRL+b, then d”.
> Note: pressing “CTRL+c” will terminate the server.

## debug command

Use debug mode to help you if you are having issues with the server. Debug allows you to see the output of the server directly to your terminal allowing you to diagnose any problems the server might be having.

````bash
./gameserver debug
````