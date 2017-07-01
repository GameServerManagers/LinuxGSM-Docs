Most admins will normally want to run multiple game servers on there Linux server. There are a couple of ways to achieve this. Depending upon the circumstances you may choose a particular method of mixture of both.

**Instance:** Each individual game server is referred too as an “instance” e.g `1.2.3.4:27015`.

**Installation:** An installation refers to the location of the games “server files” e.g `/home/csgoserver/serverfiles`.

> note: Each instance must use its own dedicated ports to function or else an instance will fail to bind correctly to a port and fail to start.

# Single instance, multiple Installations
The simplest method is to create a single installation for each instance. This will completely isolate each game server from each other. This method is useful if you run multiple game servers that have different mods or add-ons. The negatives of this include having to manage multiple installs and can take up a much larger amount of disk space.

If you are running game servers for different games you also require separate installations for each game.

## Example

|Game |User|Directory|Notes|
|--------|----|---------|-----|
| Garry’s Mod |gmodserver|/home/gmodserver|     |
| Garry’s Mod |gmodserver|/home/gmodserver-slender|Slender Man Mod|
| Counter-Strike: Global Offensive |csgoserver|/home/csgoserver|   |
| Counter-Strike: Global Offensive |csgoserver-zombies|/home/csgoserver-zombies|   |

As you can see the installs are separated and isolated from each other. If Garry’s Mod was one installation the slender man add-on may interfere with the vanilla install. 

## How to install
Simply repeat the standard installation process using a different username and location, ensuring you change the [[Ports]].

# Multiple Instances, Single Installation
Having a single installation running multiple instances is also possible. This method is great if you are running multiple vanilla game servers (of the same game) or servers that share the same add-ons. It is not recommended for servers running different mods or add-ons.

Each instance will share the same resources and add-ons meaning each instance will be affected the same by updates. This can be an advantage when updating but can also cause problems with multiple instances if add-ons break.

Every time a new instance is created new default config files are also created. This allows each instance to have a different hostname, ports etc. The config files are by default the same name as the scipt e,g if the script is `./csgoserver-2` the config is `csgoserver-2.cfg` You can see the location of config files in `./gameserver details`. Also note there are two config files, LinuxGSM configs and a game server config.

Each instance is managed using its own script. These can be called anything however the default will simply have an incremental number. Some admins may choose to use the server port instead of the incremental number.

## Example

|Game	|User	|LinuxGSM Script location|	|notes|
|--------|----|---------|-----|-------|
|Garry’s Mod|gmodserver|/home/gmodserver/gmodserver|1.2.3.4:27015
|Garry’s Mod|	gmodserver|	/home/gmodserver/gmodserver-1|	1.2.3.4:27018
|Garry’s Mod|	gmodserver|	/home/gmodserver/gmodserver-2|	1.2.3.4:27021
|Counter-Strike: Global Offensive	|csgoserver	|/home/csgoserver-zombies-27024	|1.2.3.4:27024
Zombie Mod
|Counter-Strike: Global Offensive	|csgoserver	|/home/csgoserver-zombies-27027	|1.2.3.4:27027
Zombie Mod

In this example you can see the scripts are located in the same installation but have different names. Each instance has had its port altered in the server config to prevent port clashes.

## How to install

`linuxgsm.sh` allows you to generate as many instances as you want by running `./linuxgsm.sh install`. It will generate a new LinuxGSM script using an incremental number.

For example if you already use `./csgoserver` running `./linuxgsm.sh csgoserver` will generate `./csgoserver-2`

On first run of `./gameserver-2` a new default LinuxGSM and game config will be created `gameserver-2.cfg`. These new configs will need to be altered with new ports and any other settings that are required.