# Game Server Config

{% hint style="info" %}
\_\_[_LinuxGSM Configs_](linuxgsm-config.md) and _Game Server Configs_ are different. One is the config for LinuxGSM itself and the other is for the game server instance.
{% endhint %}

Game server config files are the configuration files used by the game server to store various game server settings, such as the server name, maximum players, map cycle, etc. These settings can be edited to customise a game server. Different game server configs can use different syntax and work slightly differently, but all do the same basic job of editing a game server

## Config file's location

The `details` command will provide you with some config file information. However, some servers do use multiple config files.

### Command

`./gameserver details`

### Sample output example

```text
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
```

## LinuxGSM Custom Config's

Whenever possible, LinuxGSM provides basic easy-to-use game server configuration files.  
A dedicated repository has been made so all server admins can benefit, even Windows admins.

{% embed url="https://github.com/GameServerManagers/Game-Server-Configs" caption="" %}

This configuration file is automatically downloaded upon server installation.

## Config file naming

Whenever possible, LinuxGSM uses a custom name for configuration files that contains the `${servicename}` variable in it in order to allow the running of [multiple game servers](../features/multiple-game-servers.md) with different config files. If the game does not allow for that, then the usual name will be used.

### Example

For source servers, the default `server.cfg` is not used with LinuxGSM. Instead if you're running `./csgoserver`, then the config file will be called `csgoserver.cfg`.

## Missing configuration file handling

LinuxGSM will always check a config file is present when starting a server.  
If a config file is missing, it will re-download the default one or give a warning.

## Where are the settings I'm looking for?

Game servers have many different ways of managing settings. Some are set within [start parameters](start-parameters.md), while some are set within a configuration file.

One of the goals of LinuxGSM is to make managing these as easy as possible, by providing all important settings out of the box, wherever they are. There is no general rule about where config files are set. It is a good idea to look for the official documentation of the game server that you're trying to run in order to find relevant information about settings.

### I found missing settings or an error with config files?

If you found settings that are absent from the default configuration file provided by LinuxGSM that would be a useful addition, then you can open an issue or a pull request.

{% embed url="https://github.com/GameServerManagers/Game-Server-Configs" caption="" %}
