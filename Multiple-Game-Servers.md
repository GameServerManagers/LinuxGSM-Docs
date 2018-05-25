**There are two recommended ways to run multiple game servers on one physical server**.  
Depending upon the circumstances you may choose a particular method or mixture of both.

It is best to make a proper plan for running multiple game servers at the earliest stage of your deployment.  
Make sure that you examined this page carefully and understood all of its content before starting.

# Prerequisite

### Vocabulary

**Installation:** An installation refers to the location of the games “server files” e.g `/home/csgo/serverfiles`.

**Instance:** Each individual game server is referred too as an “instance” e.g `/home/csgo/csgoserver` would be the script for the instance called "csgoserver".

**Multiple instances:** It is possible to run multiple instances out of one single installation and to run multiple instances out of multiple installations.

### Principle of listening to an ip:port
Each service running on a machine expecting connections from a network needs to listen on an IP and port dedicated to its communication with the network. It is not possible to have multiple services listening on the same port and IP, most programs will crash if you try to do so because it cannot "bind" to an IP and port already in use.  
Therefore, each game server instance must use its own unique and dedicated [[Ports]] and/or IP to function.

Useful resource: [[Ports]]

# One user for each installation and instance

This method is the most simple and will fit most use cases.  
It consists in creating a new user for each game server.

## Use cases
* You run various game servers: they don't share any content, so it's best to isolate them into their own user
* You run multiple servers of the same game, but they need to have separate content and addons
* You want your game servers to be totally independant in order to prevent breaking everything at once and you have pently of disk space

### Pros
* Easy to setup | Just repeat the install process under a new user
* Allows full customization | Addons and server data are not shared in any way with other game servers
* More secure | If one instance gets hacked somehow, others instances on other users are intact
* More reliable | If you mess up with the game server, other ones remain untouched; in case of a game server update on one instance, you don't crash others at the same time because files changed

### Cons
* Uses more disk space | Each game server has all of the installation files
* All instances are updated separately | It will us more resources upon update and require marginally more [[Cronjobs]]

## Example

|Game Server|User|LinuxGSM Script location|
|--------|----|---------|
| Garry’s Mod |gmodserver|/home/gmodserver/gmodserver|
| Garry’s Mod |gmodserver-slender|/home/gmodserver-slender/gmodserver|
| Counter-Strike: Global Offensive |csgoserver|/home/csgoserver/csgoserver|
| Counter-Strike: Global Offensive |csgoserver-zombies|/home/csgoserver-zombies/csgoserver|

As you can see the installs are separated and isolated from each other in each user's home directory.

## How to install

Simply repeat the standard installation process using a different username and location, ensuring you change the [[Ports]] and/or IP if your server has multiple IPs. 


# Single Installation, multiple instances

This method is used when your game servers share a common base regarding mods or configuration.

## Use cases
* You want to run the same game server on different maps or game modes, you have no mods at all and want to save some disk space
* You have a server template, a common base with some mods or configuration that you want to slightly decline in different versions by using a different config file
* You're on a budget and have very limited disk space, but you just want to run multiple instances of the same game
* Your sever has a low bandwidth and you are running a lot of game servers off of it, this method will allow you to update multiple instances at once

### Pros
* Uses less disk space | Game server files, mods and addons are only installed once
* Makes less maintainance | Update one, update all of them
* Still customizable | You are able to use different config files in most cases

### Cons
* Less versatile | Each instance share the same files, so they share the same mods as well unless your mods come from a workshop collection or you can chose what mods to load in start parameters
* Less reliable | If your game server gets broken, all of your instances are down at the same time; if one instance updates, other ones might crash because files will be inconsistent regarding the expected ones
* Less secure | If your game server gets hacked somehow, all of your instances are broken at the same time

## How it works


## Example

|Game|User|LinuxGSM Script location|notes|
|--------|----|---------|-----|
|Garry’s Mod|gmodserver|/home/gmodserver/gmodserver|1.2.3.4:27015|
|Garry’s Mod|gmodserver|/home/gmodserver/gmodserver-1|1.2.3.4:27018|
|Garry’s Mod|gmodserver|/home/gmodserver/gmodserver-2|1.2.3.4:27021|
|Counter-Strike: Global Offensive|csgoserver|/home/csgoserver/csgoserver-zombies-27024|1.2.3.4:27024 Zombie Mod|
|Counter-Strike: Global Offensive|csgoserver|/home/csgoserver/csgoserver-zombies-27027|1.2.3.4:27027 Zombie Mod|

In this example, you can see the scripts are located in the same installation but have different names. Each instance has had its port altered in the server config to prevent port clashes.

## How to install

`linuxgsm.sh` allows you to generate as many instances as you want by running `./linuxgsm.sh install`. It will generate a new LinuxGSM script using an incremental number.

For example if you already use `./csgoserver` running `./linuxgsm.sh csgoserver` will generate `./csgoserver-2`

On the first run of `./gameserver-2` a new default LinuxGSM and game config will be created (`gameserver-2.cfg`). These new configs will need to be altered with new ports and any other settings that are required.

# Common mistakes

### Forgetting to change ports and/or IP
If your run multiple similar game servers, you have no choice to work on that. Read [[Ports]].

### Installing multiple game servers with the same script name under the same user
You might be tempted to have one user with one subdirectory per game servers of the same name. This won't work because each game server has a servicename defined by its "gameserver" script name. So don't try to run two scripts called "csgoserver" under the same user, they will conflict. If you are using whole different game server, it's best to isolate them under a different user, but if you have no choice (for example on a shared machine), then you should rename each game server script, and of course, make sure you are using different ports for each server, and that your desired ports are not in use by another user of the machine.