# ARK: Survival Evolved

![ARK Logo](../.gitbook/assets/header-1.jpg)

## Server Resources

-   [Official Dedicated Server Guide](https://ark.wiki.gg/wiki/Dedicated_server_setup)
-   [Official Dedicated Server Configuration](https://ark.wiki.gg/wiki/Server_configuration)
-   [Steam Workshop](https://steamcommunity.com/app/346110/workshop/)
-   [Official ARK: Survival Evolved Server Administration forum](https://survivetheark.com/index.php?/forums/forum/39-server-administration/)

## System Requirements

Different Maps require different system requirements.

-   TheIsland: 7GB RAM
-   Genesis 2: 12GB RAM

## Config Files

An example of GameUserSettings.ini can be found [here](https://github.com/GameServerManagers/Game-Server-Configs/blob/main/ark/GameUserSettings.ini).

```text
serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
```

## Server Settings

{% hint style="info" %}
Command line parameters take precedence over configuration files.
{% endhint %}

### Common Command-Line Parameters

Below is a list of common Command-Line parameters. For a complete list see the [Ark Wiki](https://ark.wiki.gg/wiki/Server_configuration#Command_line_options).

| Parameter                             | Description                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SessionName                           |                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -MultiHome                            | Enables multihoming.                                                                                                                                                                                                                                                                                                                                                                                                      |
| -Port                                 |                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -QueryPort                            |                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -AutoManagedMods                      | Steam only, automatic MOD download/installation/updating. Mod IDs are listed in _Game.ini_ under `[ModInstaller]` section.                                                                                                                                                                                                                                                                                                |
| -CrossPlay                            | Enables crossplay (i.e.: EPIC and Steam) on dedicated server. Note: PublicIPForEpic must also be set.                                                                                                                                                                                                                                                                                                                     |
| -PublicIPForEpic=\<IPAddress>         | This is the public IP that EGS clients will attempt to connect to, if this option is missing and `-MULTIHOME` is specified, then EGS clients will attempt to connect to the multihome IP; note that if you're using multihome and specify a non-public IP address, then players will not be able to connect to your server using EGS. Make sure to set a public IP address (e.g.: WAN or external).                       |
| -NoBattlEye                           | Run server without BattleEye.                                                                                                                                                                                                                                                                                                                                                                                             |
| -ActiveEvent=                         | Enables a specified event or enables the event's colour palette on wild creatures. Only one can be specified and active at a time.                                                                                                                                                                                                                                                                                        |
| ?AltSaveDirectoryName=\<savedir_name> | Allows to specify a custom directory name for server world-save. Usually used to manage clusters, read more about it in the [Cross-ARK Data Transfer](https://ark.wiki.gg/wiki/Server_configuration#Cross-ARK_Data_Transfer) section.                                                                                                                                                                                     |
| -insecure                             | Disable Valve Anti-Cheat (VAC) system.                                                                                                                                                                                                                                                                                                                                                                                    |
| -MapModID=                            | Dedicated servers can now optionally load custom maps via `ModID` directly, rather than having to specify the map name, using this syntax (where the `MapModID` is the Steam Workshop ID of your custom map, and the GameModIds are the Id’s of the stacked mods you wish to use, in order). `ActiveMods` must also be set in [GameUserSettings.ini](https://ark.wiki.gg/wiki/Server_configuration#GameUserSettings.ini). |
| ?GameModIds=\[,\[...]]                | Steam only. Specifies the order and which mods are loaded, `ModIDs` need to be separated with commas (`,`). Mod priority is in descending order left to right (the left-most ID is the top priority mod). It is suggested to use instead the `ActiveMods` under `[ServerSettings]` of _GameUserSettings.ini_.                                                                                                             |

### Common Configuration File Settings

Below is a list of common Configuration settings. For a complete list see the [Ark Wiki](https://ark.wiki.gg/wiki/Server_configuration#Configuration_Files).

The following options must come under the `[ServerSettings]` section of `GameUserSettings.ini`:

| Variable                                         | Description                                                                                                                        |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| ActiveMods=ModID1,ModID2,ModID3                  | Value type: list of mod IDs, comma-separated with no spaces, in a single line (for example: `ModID1,ModID2,ModID3`)                |
| BanListURL="http://arkdedicated.com/banlist.txt" | Value type: string with a URL Sets the global ban list. Must be enclosed in double-quotes. </p>                                    |
| RCONEnabled=True                                 | f `True`, enables RCON, needs `RCONPort=<TCP_PORT>` and `ServerAdminPassword=<admin_password>` to work                             |
| RCONPort=27020                                   | Specifies the optional TCP RCON Port.                                                                                              |
| ServerAdminPassword=                             | If specified, players must provide this password (via the in-game console) to gain access to administrator commands on the server. |
| ServerPassword=                                  | If specified, players must provide this password to join the server.                                                               |
| serverPVE=                                       | If `True`, disables [PvP](https://ark.wiki.gg/wiki/PvP) and enables [PvE](https://ark.wiki.gg/wiki/PvE)                            |

The following options must come under the `[SessionSettings]` section of `GameUserSettings.ini`.

| Variable    | Description                                                                                                                                                                                   |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SessionName | Specifies the Server name advertised in the Game Server Browser as well in Steam Server browser. If no name is provided, the default name will be _ARK #_ followed by a random 6 digit number |

The following options must come under the `[/Script/Engine.GameSession]` section of `GameUserSettings.ini`.

| Variable      | Description                                                                         |
| ------------- | ----------------------------------------------------------------------------------- |
| MaxPlayers=70 | Specifies the maximum number of players that can play on the server simultaneously. |

The section `[ModInstaller]` handles each extra Steam Workshop Mods/Maps/TC IDs in the `Game.ini`.

| Variable          | Description                                                                                                                                                                                                                                                     |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ModIDS=\<integer> | Specifies a single Steam Workshop Mods/Maps/TC ID to download/install/update on the server. To handle multiple IDs, multiple lines must be added with the same syntax, each one with the specific workshop ID. Requires `-automanagedmods` in the command line. |

## Alt Saved Directory Name

```text
altsavedirectoryname=
```

The `altsavedirectoryname` is the location where the game save will be stored. By default, this is the current map name. However, this setting can be customised if desired.

{% hint style="warning" %}
Be careful not to accidentally overwrite a save file if changing maps or using a custom save location.
{% endhint %}

If `altsaveddirectoryname` is `TheIsland` the save is located will be:

```text
ShooterGame/Saved/TheIsland
```

## Official Map Names

-   TheIsland
-   TheCenter
-   ScorchedEarth_P
-   Ragnarok
-   Aberration_P
-   Extinction
-   Valguero_P
-   Genesis
-   CrystalIsles
-   Gen2
-   LostIsland
-   Fjordur
-   PGARK

## Mod Support

ARK server mods are managed using the [Steam Workshop](https://steamcommunity.com/app/346110/workshop/), this allows the auto-install and update of mods.

### Adding Mods

Firstly, you need to select the mods you want to use from the [Steam Workshop](https://steamcommunity.com/app/346110/workshop/).

{% hint style="warning" %}
Mods can cause your server to become unstable or may not be compatible with each other. It is a good idea to read the mods docs and/or speak with other experienced ARK admins.
{% endhint %}

Here is a simple mod to get started:

-   [Editable Server UI (WBUI) Open Source - 924619115](https://steamcommunity.com/sharedfiles/filedetails/?id=924619115)

`-AutoManagedMods` is the required [parameter](../configuration/start-parameters.md) to add workshop support and is added to the start parameters by default.

Edit `GameUserSettings.ini`, adding the following line under `[ServerSettings]`. To add multiple mods use a comma delimiter e.g `ActiveMods=924619115,924619652`.

```text
[ServerSettings]
ActiveMods=924619115
```

Next, edit or create `Game.ini` and add the following section, this will enable the auto-download of mods. To add multiple mods add another `ModIDS=` line underneath the first.

```text
[ModInstaller]
ModIDS=924619115
```

For the example mod add the following to `GameUserSettings.ini` other mods may require their own configuration as per their documentation.

```text
[WBUI]
Icon=1
OpenBtn=0
HideBuff=true
HideAfter=60
TribeTab=true
OpenOnStart=true
OnlyNewPlayers=true
UseJson=false
JsonURL="https://dl.dropboxusercontent.com/s/6rhwbq95wwm5gkd/UI.json"
UpdateInterval=24
```

For more config options for WBUI see this [link](https://steamcommunity.com/workshop/filedetails/discussion/924619115/129069130858283275).

Start the server and the mods will be automatically downloaded by the server. To check that this has worked open the console `./arkserver console`. In the console, you will see a message similar to the following.

{% hint style="info" %}
Large mods may take several minutes to download to the server.
{% endhint %}

```text
Using binned.
4.5.1-0+UE4 7038 3077 404 10
[S_API FAIL] SteamAPI_Init() failed; SteamAPI_IsSteamRunning() failed.
Setting breakpad minidump AppID = 346110
Redirecting stderr to '/home/lgsm/.steam/logs/stderr.txt'
[  0%] Checking for available updates...
[----] Verifying installation...
Steam Console Client (c) Valve Corporation
-- type 'quit' to exit --
Loading Steam API...Failed to init SDL priority manager: SDL not found
Failed to set thread priority: per-thread setup failed
Failed to set thread priority: per-thread setup failed
OK.

Connecting anonymously to Steam Public...Loaded client id: 13529975768029855698
Listening for IPv4 broadcast on: 27036
Logged in OK
Waiting for user info...OK
Downloading item 679529026 ...
Success. Downloaded item 679529026 to "/home/lgsm/.steam/SteamApps/workshop/content/346110/679529026" (1365998905 bytes)
```

If you join before the server or your client has fully downloaded the mod you might get a _Mod Version Mismatch_ error. Simply, give the server more time to load the mods.

![Screenshot](../.gitbook/assets/gpwwd19-1.png)

Once you have connected to the server you will be able to see that the mod has loaded by seeing the _Mod Name_ in the game menu `Esc`.

![Screenshot](<../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

The example mod can be activated by pressing `F1`.

![Screenshot](../.gitbook/assets/924619115_preview_unbenannt.PNG)

### Mod Collections

The Steam Workshop has a feature that allows mods to be grouped in collections. Currently, Steam workshop collection IDs won't work directly with ARK. Instead, you need to have all the individual IDs of the mods you want to use.

{% hint style="info" %}
To get individual item IDs from collections you can use the [Steam Collection ID Grabber](https://tools.rusty.info/tools/stcolids/).
{% endhint %}

## IP Addressing

### Multihome&#x20;

The `-MultiHome` parameter is used to bind the server to a specific interface. By default, LinxuGSM sets this to the `${ip}` variable.

### PublicIPForEpic

If you want players who use the Epic Store to connect to the server the `-PublicIPForEpic` parameter. By default, LinuxGSM will set this to the `${publicip}` variable.

## Multi-Instance

ARK can work with LinuxGSM [multi instances](../configuration/multiple-game-servers.md)in the same install. However, each instance will use the same `GameUserSettings.ini`. To customise each server use command-line parameters as they take precedence over the configs.

## CrossARK (Clusters)

A [CrossARK](https://ark.wiki.gg/wiki/CrossARK_Transfers) cluster allows players to transfer a survivor, items, and tames ("objects") from one ARK to another ARK. A server admin can group all their ARK servers together in a cluster. Typically a server admin will cluster servers with different maps. There are a few different ways to configure CrossARK depending upon your configuration.

### Cluster ID

&#x20;The cluster ID is the global name of the cluster. Each instance that will be attached to the cluster must have the same cluster ID. Use `-ClusterId=<CLUSTER NAME>`to specify the cluster ID.

### Cluster Directory

Each server instance must be able to access the _cluster directory_. The cluster directory is a shared location that allows survivor and other data to be shared between server instances.

By default the cluster directory is `ShooterGame/Saved/clusters/<CLUSTER NAME>`. Depending upon your configuration it may be required that instances need to be pointed to a specific shared directory. To do this use add the`-ClusterDirOverride=<PATH>` parameter with the directory location.&#x20;

The shared directory can be any preferred location however each instance must be able to read and write to that directory.

### Game Server Instance locations

It is possible to set up clusters between game server instances in the same installation directory, separate installation directory, or even separate physical servers as long as all instances can access the cluster directory.

Using multiple physical servers will require the use and configuration of a file-sharing or syncing software such as SAMBA, Syncthing, or rsync.

### Adding Servers to Clusters

Firstly, set up [multiple ARK game server instances](../configuration/multiple-game-servers.md).

In the below example, 2 servers will be clustered together in the same instance. For CrossARK to work each instance must have the same cluster id and share the same cluster directory.

{% hint style="info" %}
If you have multiple separate installations of ARK use `-ClusterDirOverride` to point each installation to the same cluster directory.
{% endhint %}

Change the command-line parameters for your server instances by editing the instance configs.

#### Server 1 (**arkserver.cfg)**

```bash
port="7777"
queryport="27015"
rconport="27020"
defaultmap="TheIsland"
```

```bash
${defaultmap}?SessionName=LinuxGSM-Server-1?AltSaveDirectoryName=${altsavedirectoryname}?RCONPort=${rconport} -MultiHome=${ip} -Port=${port} -QueryPort=${queryport} -AutoManagedMods -Crossplay -PublicIPForEpic=${publicip} -ClusterId=hsqCd8MR65VFRFdPcDjw
```

#### **Server 2 (arkserver-2.cfg)**

```bash
port="7778"
queryport="27016"
rconport="27021"
defaultmap="Ragnarok"
```

```bash
${defaultmap}?SessionName=LinuxGSM-Server-2?AltSaveDirectoryName=${altsavedirectoryname}?RCONPort=${rconport} -MultiHome=${ip} -Port=${port} -QueryPort=${queryport} -AutoManagedMods -Crossplay -PublicIPForEpic=${publicip} -ClusterId=hsqCd8MR65VFRFdPcDjw
```

Once both server instances have been started check that the cluster directory has been created in `ShooterGame/Saved/clusters/hsqCd8MR65VFRFdPcDjw`.&#x20;

{% hint style="info" %}
This may require you to connect to an instance first
{% endhint %}

{% hint style="warning" %}
Servers that are running on _local networks_ sometimes have trouble traveling to other arks. A potential fix for this is adding `MultiHome=0.0.0.0` to your command-line parameters.
{% endhint %}
