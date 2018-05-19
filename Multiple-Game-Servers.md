There are a couple of ways to achieve running multiple game server on one physical server.  
Depending upon the circumstances you may choose a particular method or mixture of both.

# Prerequisite

### Vocabulary

**Installation:** An installation refers to the location of the games “server files” e.g `/home/csgo/serverfiles`.

**Instance:** Each individual game server is referred too as an “instance” e.g `/home/csgo/csgoserver` would be the script for the instance called "csgoserver".

**Multiple instances:** It is possible to run multiple instances out of one single installation and to run multiple instances out of multiple installations.

### Principle of listening to an ip:port
Each service running on a machine expecting connections from a network needs to listen on an IP and port dedicated to its communication with the network. It is not possible to have multiple services listening on the same port and IP, most programs will crash if you try to do so because it cannot "bind" to an IP and port already in use.  
Therefore, each game server instance must use its own unique and dedicated [[Ports]] and/or IP to function.

Useful resource: [[Ports]]

# One instance per installation
This method consists in creating a new user for each game server. It is useful if you run multiple game servers that have different mods or add-ons, or if you have plenty of disk space and just want the easiest and safest way to proceed.

**Pros**
* Easy to setup
* Allows full customization
* More secure and reliable

**Cons**
* Uses more disk space

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

**Pros**
* Uses less disk space
* Makes less maintainance
* Still able to use different config files in most cases

**Cons**
* Each instance share the same files, so they share the same mods as well
* If your game server gets broken, all of your instances are broken at the same time

Every time a new instance is created new default config files is also created. This allows each instance to have a different hostname, ports etc. The config files are by default the same name as the script. For example, if the script is `./csgoserver-2` the config is `csgoserver-2.cfg`. You can see the location of config files in `./gameserver details`. Also note there are two config files, LinuxGSM configs and a game server config.

Each instance is managed using its own script. These can be called anything, however, the default will simply have an incremental number. Some admins may choose to use the server port, the map or the gamemode instead of the incremental number.

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
If your run multiple similar game servers, you have no choice to work on that. Read [[Port]].

### Installing multiple game servers with the same script name under the same user
You might be tempted to have one user with one subdirectory per game servers of the same name. This won't work because each game server has a servicename defined by its "gameserver" script name. So don't try to run two scripts called "csgoserver" under the same user, they will conflict.