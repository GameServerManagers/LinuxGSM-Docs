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

For more info, see [[LinuxGSM Config Files]].

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

For more info, see [[Start-Parameters]].
 
# Updating a Game Server
Most game servers receive regular updates the game developers. These servers can be updated automatically using the update feature.

## update command

The [[update]] command checks if an update is available for the server. The server will update and restart only if required.
````bash
./gameserver update
````
For more info, see [[update]]

## validate command

For SteamCMD servers only, the [[validate]] command checks the integrity of server files to make sure files are not corrupt and match the remote version. This can be useful if an update fails or the server is frequently crashing.

````bash
./gameserver validate
````
For more info, see  [[validate]]

# Updating LinuxGSM
LinuxGSM is regularly updated with various enhancements and fixes; Because of this the LinxuGSM updater is available. For more info, see [[update-lgsm]].

````bash
./gameserver update-lgsm
````
For more info, see [[update-lgsm]]

# Automating tasks

You can use [[Cronjobs]] to automate any LinuxGSM command.
Most commonly used are:
* Automatically check for updates. [[update]]
* Automatically check for server crash and restart if needed. [[monitor]]
* Automatically keep LinuxGSM up to date. [[update-lgsm]]
* Automatically restart the server at a given time. [[start-stop-restart]]
* Automatically update and restart the server. [[force-update]]
* Automatically backup the server. [[backup]]

For more details, see [[Cronjobs]].

## Running on Boot
To run a server [[On-Boot]], using a monitor cronjob is recommended; any server that was online before a machine reboot will be restarted. 

For more info, see [[On-Boot]] or [[Monitor#automated-monitoring]].

# Troubleshooting

## Logs

Various logs are available. They can help you checking for your server's health and diagnosing issues.

Logs location: `log/`

For more info, see [[Logging]].

## console command

The [[console]] command allows you to view the live console of a running server and to enter commands (if available). If the game offers a good console output, it could help diagnose issues along with logs.

````bash
./gameserver console
````

To exit the console press “CTRL+b, then d”.
> Note: pressing “CTRL+c” will terminate the server.

For more info, see [[console]].

## debug command

Use debug mode to help you if you are having issues starting the server. Debug allows you to see the output of the server directly to your terminal allowing you to diagnose any problems the server might be having.

````bash
./gameserver debug
````

See [[debug]].