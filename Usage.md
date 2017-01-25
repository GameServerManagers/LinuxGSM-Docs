Here is an overview of how to use LGSM. For more advanced details on a feature see the feature page.

**Note**: Replace generic "gameserver", "gamename", and "username" from these examples by your actual script, game, and user names.

# Installing

First visit the game server page of your choice [gameservermanagers.com](http://gameservermanagers.com/).
Follow basic instructions from it:
- Install required packages (dependencies) as shown onto the website.  
- Make a new user and login into it.
- Download the script, make it executable, then install the server with `./gameserver install`.

# Available commands

To see a list of available commands, just execute your "gameserver" script with no argument.

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

You will find a wiki page for every single command if needed. We will go through some of them here anyways.

# Running your server

To [[start-stop-restart]] your server, use the following commands:

````bash
./gameserver start
./gameserver stop
./gameserver restart
````

# Getting server and machine information

The [[details]] command will provide you with config file's location, start parameters settings, and many other information. Feel free to use it as much as needed!

````bash
./gameserver details
````

# Configuring your server

Your server starts, great! You might now want to customize some settings.

## Config Files

Most servers use a configuration file to alter most settings.  
Whenever possible, LinuxGSM provides an enhanced default config file from https://github.com/GameServerManagers/Game-Server-Configs
If there is one, the [[details]] command will provide you with config file's location.

````bash
./gameserver details
````
Sample output: 
````
Config file:   /home/username/serverfiles/gamename/cfg/gamename-server.cfg
````
You can edit this file with any Linux text editor like `nano` or `vi`.

LGSM does not provide specific information about altering this configuration file except for some special games showed in "Game Info" section from the [wiki](https://github.com/GameServerManagers/LinuxGSM/wiki). There are also many websites that provide documentation and support on configuring your server.

## Start Parameters & LGSM Settings

Servers commonly require [[Start-Parameters]] to set some settings.
Start parameters are command line options appended to server's executable when you start it.  
These parameters can again be reviewed using the [[details]] command.  
To alter them, you will need to edit the main `gameserver` script file using `vi` or `nano` and edit variables from the `## Server Start Settings` section.
You will also find the `#### LinuxGSM Settings ####` section, allowing you to customize many different behaviors.

````bash
nano gameserver
````

There are many possible settings set through start parameters. The best thing to do is to check your script file and see if there are any that you'd like to alter. Whenever possible, a wiki link is provided to provide you with information about the command.

# Updating your server

Most servers can be updated automatically using the update feature which uses SteamCMD.

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

# Automating tasks

You can use [[Cronjobs]] to automate any LGSM function.
Most used ones are:
* Automatically check for updates [[update]]
* Automatically check for server crash and restart if needed [[monitor]]
* Automatically keep LGSM up to date [[update-functions]]
* Automatically restart the server at a given time [[start-stop-restart]
* Automatically update and restart the server [[force-update]]
* Automatically backup the server [[backup]]

For more details, see [[Cronjobs]]

## Running on Boot
To run a server [[On-Boot]], we advise to use a monitor cronjob: any server that was online before a machine reboot will be restarted. 

See [[On-Boot]] or [[Monitor#automated-monitoring]] for more information.

# Troubleshooting

## Logs

Script (LGSM) and game console logs are available. They can help you checking for your server's health and diagnosing issues.

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

# Updating your LGSM script
LGSM has the ability to self [update-functions].

````bash
./gameserver update-functions
````

This will allow you to get various fixes and possibly new functionalities.  
In some rare cases, you will need to update your main "gameserver" script as well in order to enjoy all new functionalities.