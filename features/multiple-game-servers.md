# Multiple Game Servers

**There are two recommended ways to run multiple game servers on one physical server**.  
Depending upon the circumstances you may choose a particular method or mixture of both.

It is best to make a proper plan for running multiple game servers at the earliest stage of your deployment.  
Make sure that you examined this page carefully and understood all of its content before starting.

## Prerequisite

#### Vocabulary

You need some definitions to make this guide clear.

* **Installation:** An installation refers to the location of the games “server files” e.g `/home/csgo/serverfiles`.
* **Instance:** Each individual game server is referred too as an “instance” e.g `/home/csgo/csgoserver` would be the script for the instance called "csgoserver".
* **Multiple instances:** It is possible to run several instances out of one single installation and to run several instances out of multiple installations.

#### LinuxGSM Configuration

You need to be comfortable with [LinuxGSM Config](../configuration/linuxgsm-config.md).

#### Understand ports

You need to understand how ports and service listening work in order to avoid port overlapping, otherwise your new instances won't start. Useful resource: [Ports](../configuration/ports.md).

## One user for each installation and instance

This method is the most simple and will fit most use cases.  
It consists of creating a new user for each game server, repeat the install process and edit your [LinuxGSM Config](../configuration/linuxgsm-config.md) if needed.

### Use cases

* You run various game servers: they don't share any content, so it's best to isolate them into their own user
* You run multiple servers of the same game, but they need to have separate content and addons
* You want your game servers to be totally independent in order to prevent breaking everything at once, also, you have plenty of free disk space

#### Pros

* Easy to setup \| Just repeat the install process under a new user
* Allows full customization \| Addons and server data are not shared in any way with other game servers
* More secure \| If one instance gets hacked somehow, others instances on other users are intact
* More reliable \| If you mess up with the game server, other ones remain untouched; in case of a game server update on one instance, you don't crash others at the same time because files changed

#### Cons

* Uses more disk space \| Each game server has all of the installation files
* All instances are updated separately \| It will use more resources upon update and require marginally more [Cronjobs](../configuration/cronjobs.md)

### Example

| Game Server | User | LinuxGSM Script location |
| :--- | :--- | :--- |
| Garry’s Mod | gmodserver | /home/gmodserver/gmodserver |
| Garry’s Mod | gmodserver-slender | /home/gmodserver-slender/gmodserver |
| Counter-Strike: Global Offensive | csgoserver | /home/csgoserver/csgoserver |
| Counter-Strike: Global Offensive | csgoserver-zombies | /home/csgoserver-zombies/csgoserver |

As you can see the installs are separated and isolated from each other in each user's home directory.

### How to install

1\) Create a new user with a home directory. 2\) Repeat the standard installation process using this different user. 3\) If your game server uses the same default [Ports](../configuration/ports.md) as a previously installed one, make sure you change them \(and/or IP if your server has multiple IPs\) in you [LinuxGSM Config](../configuration/linuxgsm-config.md) or in [Game Server Config](../configuration/game-server-config.md) depending on the game server you run.

## Single Installation, multiple instances

This method is used when your game servers share a common base regarding mods or configuration. LinuxGSM is helping a lot with this kind of configuration with many useful features as you will see.

### Use cases

* You want to run the same game server on different maps or game modes, you have no mods at all and want to save some disk space
* You have a server template, a common base with some mods or configuration that you want to slightly decline in different versions by using a different config file
* You're on a budget and have very limited disk space, but you just want to run multiple instances of the same game
* Your server has a low bandwidth and you are running a lot of game servers off of it, this method will allow you to update multiple instances at once

#### Pros

* Uses less disk space \| Game server files, mods and addons are only installed once
* Makes less maintenance \| Update one, update all of them
* Still customizable \| You are able to use different config files in most cases

#### Cons

* Less versatile \| Each instance share the same files, so they share the same mods as well unless your mods come from a workshop collection or you can choose what mods to load in start parameters
* Less reliable \| If your game server gets broken, all of your instances are down at the same time; if one instance updates, other ones might crash because files will be inconsistent regarding the expected ones
* Less secure \| If your game server gets hacked somehow, all of your instances are broken at the same time

### How it works: concept

You have one game server installed, but you will have multiple scripts \(called "instances"\) to start the same installation but with different config files.  
Every time a new instance is created, new default config files are also created. This allows each instance to have different hostname, ports etc. The config files are by default the same name as the instance script. For example, if the script is `./csgoserver-2` the config is `csgoserver-2.cfg`. You can see the location of config files in `./instance details` \(replace "instance" with your actual instance name\).

There are two types of config files: [LinuxGSM Config](../configuration/linuxgsm-config.md) and [Game Server Config](../configuration/game-server-config.md).  
And there are three levels of LinuxGSM config files, helping with managing multiple instances of the same installation. See [LinuxGSM Config](../configuration/linuxgsm-config.md) for more details.

Each instance is managed using its own script which gives the config file names. These can be renamed how you like, however, the default will simply have an incremental number. Some admins may choose to name them after the server port, the map or the gamemode instead.

### Example

| Game | User | LinuxGSM Script location | notes |
| :--- | :--- | :--- | :--- |
| Garry’s Mod | gmodserver | /home/gmodserver/gmodserver | 1.2.3.4:27015 |
| Garry’s Mod | gmodserver | /home/gmodserver/gmodserver-1 | 1.2.3.4:27018 |
| Garry’s Mod | gmodserver | /home/gmodserver/gmodserver-2 | 1.2.3.4:27021 |
| Counter-Strike: Global Offensive | csgoserver | /home/csgoserver/csgoserver-zombies-27024 | 1.2.3.4:27024 Zombie Mod |
| Counter-Strike: Global Offensive | csgoserver | /home/csgoserver/csgoserver-zombies-27027 | 1.2.3.4:27027 Zombie Mod |

In this example, you can see the scripts are located in the same installation but have different names. Each instance has had its port altered in the server config to prevent port clashes.

### How to install

`linuxgsm.sh` allows you to generate as many instances as you want by running `./linuxgsm.sh install`. It will generate a new LinuxGSM script using an incremental number.

For example if you already use `./csgoserver` running `./linuxgsm.sh csgoserver` will generate `./csgoserver-2`

On the first run of `./gameserver-2` a new default LinuxGSM and game config will be created \(`gameserver-2.cfg`\). These new configs will need to be altered with new ports and any other settings that are required.

## Common mistakes

### Forgetting to change ports and/or IP

If you run multiple similar game servers, you have no choice to work on that. Read [Ports](../configuration/ports.md).

### Installing multiple game servers with the same script name under the same user

You might be tempted to have one user with one subdirectory per game servers of the same name. This won't work because each game server has a servicename defined by its "gameserver" script name. So don't try to run two scripts called "csgoserver" under the same user, they will conflict. If you are using whole different game server, it's best to isolate them under a different user, but if you have no choice \(for example on a shared machine\), then you should rename each game server script, and of course, make sure you are using different ports for each server, and that your desired ports are not in use by another user of the machine.

