---
description: Hosting multiple game servers on the same host
---

# Running Multiple Game Servers

Depending upon the game server you are running it is possible to run multiple game servers on the same server host.

**There are two recommended ways to run multiple game servers on one physical server**.\
Depending upon the circumstances you may choose a particular method or mixture of both.

It is best to make a proper plan for running multiple game servers at the earliest stage of your deployment.\
Make sure that you examine this page carefully and understand all of its content before starting.

## Prerequisites

### Vocabulary

You need some definitions to make this guide clear.

-   **Installation:** An _installation_ refers to the base directory of a game server. This is where the files required to run a game server is stored.

```text
/home/gameserver/serverfiles
```

-   **Instance:** Each individual game server is referred to as an _instance._ There might be multiple instances running per installation. An instance is started by running the `./gameserver` script

```text
/home/gameserver/gameserver
/home/gameserver/gameserver-2
```

-   **User:** Each game server installation should run using its own _Linux user_. Although it is possible to have multiple _installations_ per user.

#### LinuxGSM Configuration

You should be familiar with how [LinuxGSM Configs](linuxgsm-config.md) work.

#### Understand ports

You need to understand how ports work in order to avoid port overlapping, otherwise, your new instances won't start. Useful resource: [Ports](../networking/ports.md).

## Single Instance per Installation

Single instance per installation is the most simple method and will fit most use cases. It keeps the server files and configs completely separate from each other.

This consists of creating a new user for each game server, repeating the install process, and edit your config files ensuring default ports are changed.

### Use cases

-   Running different game servers requires installation in a different directory
-   Running multiple servers of the same game, but they have different content, addons or mods.
-   You want your game servers to be totally separate for simplicity and reduce the chance of multiple instances breaking all at once.

#### Pros

-   Easy to setup
-   Separate installations partition the game servers from each other
-   Each instance can have different maps, addons and mods rather than sharing, preventing conflicts.
-   More secure, by keeping instances separate with there own user.
-   Reduced risk of breaking multiple instances.

#### Cons

-   Requires more disk space as server files can not be shared
-   Each instance has to be individually setup.

### Examples

The installs are separated and isolated from each other in each users _home directory_.

| Game Server                      | User               | LinuxGSM Script location            |
| -------------------------------- | ------------------ | ----------------------------------- |
| Garry's Mod                      | gmodserver         | /home/gmodserver/gmodserver         |
| Garry's Mod                      | gmodserver-slender | /home/gmodserver-slender/gmodserver |
| Counter-Strike: Global Offensive | csgoserver         | /home/csgoserver/csgoserver         |
| Counter-Strike: Global Offensive | csgoserver-zombies | /home/csgoserver-zombies/csgoserver |

### How to Install

1. Create a new user with a home directory.&#x20;
2. Repeat the standard installation process using this new user.
3. Change the instance config adjusting ports numbers from the default&#x20;

## Single Installation with Multiple Instances

Single installation with multiple instances is the method used when base installation content, maps, addons and mods are the same. Allowing either a clone of an existing instance or using different slightly different config such as different game modes and map rotations.

This consists of creating a new LinuxGSM executable file `./gameserver-2` in the same installation as an existing instance.

{% hint style="danger" %}
Most but not all game servers work with this method
{% endhint %}

### Use cases

-   Running cloning an existing game server by creating a new instance.
-   Running the same game server with different game modes, maps etc.
-   Running multiple instances even with limited disk space available.

#### Pros

-   Uses less disk space as base installation is the same
-   Less configuration required
-   It is possible to use different game modes and map rotations by editing configs.

#### Cons

-   Each instance shares the same files which may limit options to customise an instance
-   Potential mod conflicts
-   Should one instance break all instances might also experience the same issue

### How it works

You have one game server installation, but you have multiple instances start in the same installation using different config files.&#x20;

Every time a new instance is created, new default config files are created. This allows each instance to have different hostname, ports etc. The config files are by default the same name as the instance script. For example, if the script is `./gameserver-2` the config is `gameserver-2.cfg`. You can see the location of config files in `./gameserver-2 details` (replace "instance" with your actual instance name).

Each instance is managed using its own script which gives the config file names. These can be renamed how you like, however, the default will simply have an incremental number. Some admins may choose to name them after the server port, the map or the gamemode instead.

### Examples

| Game                             | User       | LinuxGSM Script location                  | notes                    |
| -------------------------------- | ---------- | ----------------------------------------- | ------------------------ |
| Garry's Mod                      | gmodserver | /home/gmodserver/gmodserver               | 1.2.3.4:27015            |
| Garry's Mod                      | gmodserver | /home/gmodserver/gmodserver-1             | 1.2.3.4:27018            |
| Garry's Mod                      | gmodserver | /home/gmodserver/gmodserver-2             | 1.2.3.4:27021            |
| Counter-Strike: Global Offensive | csgoserver | /home/csgoserver/csgoserver-zombies-27024 | 1.2.3.4:27024 Zombie Mod |
| Counter-Strike: Global Offensive | csgoserver | /home/csgoserver/csgoserver-zombies-27027 | 1.2.3.4:27027 Zombie Mod |

In these examples, you can see the scripts are located in the same installation but have different names. Each instance has had its port altered in the server config to prevent port clashes.

### How to install

`linuxgsm.sh` allows you to generate as many instances as you want by running .&#x20;

```bash
./linuxgsm.sh install
OR
./linuxgsm.sh gameserver
```

It will generate a new LinuxGSM script using an incremental number.

```bash
./gameserver-2
```

On the first run of `./gameserver-2` a new default LinuxGSM and game config `gameserver-2.cfg`will be created . These new configs will need to be altered with new ports, hostname and any other settings that are required.

## Common Mistakes

### Forgetting to change ports and/or IP

If you run multiple game servers you will need to alter ports. Ensure you are aware of how to manage [ports](../networking/ports.md).

### Installing game servers with the same script name under the same user

Installing multiple installations using the same user does work. However you must use unique script names i.e. `./gameserver`. This is because tmux requires unique session name to start a session. Tmux will fail to start if another server is using the same session name. LinuxGSM uses the script name as the tmux session name.
