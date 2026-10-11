# Workshop

Many Steam games support the [Steam Workshop](https://steamcommunity.com/workshop), an easy way to share community-made maps, game modes, mods, skins and other content.

On game servers, the Workshop makes community content (mainly maps, game modes and mods) available to play. For most games, players who connect download the content automatically, which removes the need for a [FastDL](../commands/fastdl.md) server.

Game servers get Workshop content in one of two ways:

* **The game server downloads it.** You add item or collection IDs to the game server config or start parameters, and the server downloads them when it starts. LinuxGSM adds the settings to its config where they are available.
* **LinuxGSM downloads it.** Some game servers cannot download Workshop content themselves. For these, LinuxGSM downloads the content with SteamCMD, installs it and keeps it up to date with the [workshop-update](../commands/workshop-update.md) command. See [LinuxGSM Workshop Downloads](#linuxgsm-workshop-downloads).

## Supported Game Servers

| Game server | Downloaded by | Where to add Workshop content |
| --- | --- | --- |
| [ARK: Survival Evolved](../game-servers/ark-survival-evolved.md) | Game server | `ActiveMods=` in `GameUserSettings.ini` (`-AutoManagedMods` is in the default start parameters) |
| [Arma 3](../game-servers/arma-3.md) | LinuxGSM (v26.4.0+) | `workshopmods` in the [LinuxGSM config](../configuration/linuxgsm-config.md) |
| Barotrauma | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Colony Survival | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| [Counter-Strike 2](../game-servers/counter-strike-2.md) | Game server | `+host_workshop_collection` or `+host_workshop_map` in `startparameters`, with `wsapikey` set |
| [Counter-Strike: Global Offensive](../game-servers/counter-strike-global-offensive.md) | Game server | `wscollectionid`, `wsstartmap` and `wsapikey` in the LinuxGSM config |
| Day of Infamy | Game server | `subscribed_file_ids.txt` in the game directory (`-workshop` is in the default start parameters) |
| DayZ | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| [Don't Starve Together](../game-servers/dont-starve-together.md) | Game server | `dedicated_server_mods_setup.lua` |
| [Garry's Mod](../game-servers/garrys-mod/README.md) | Game server | `wscollectionid` in the LinuxGSM config |
| Insurgency | Game server | `subscribed_file_ids.txt` in the game directory (`-workshop` is in the default start parameters) |
| [Killing Floor 2](../game-servers/killing-floor-2.md) | Game server | `ServerSubscribedWorkshopItems` in `LinuxServer-KFEngine.ini` |
| Left 4 Dead 2 | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Natural Selection 2 | Game server | `-mods` in `startparameters` (`mods` in the LinuxGSM config for NS2: Combat) |
| Operation: Harsh Doorstop | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Project Zomboid | Game server | `WorkshopItems=` and `Mods=` in the server `.ini` |
| Squad | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Squad 44 | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Starbound | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Stationeers | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config |
| Unturned | Game server | `WorkshopDownloadConfig.json` |

{% hint style="info" %}
[Insurgency: Sandstorm](../game-servers/insurgency-sandstorm.md) uses [mod.io](https://mod.io), not the Steam Workshop.
{% endhint %}

## Items and Collections

The Steam Workshop is made up of individual items, such as maps, game modes and mods, and collections of items. Game servers download them by their ID number. For collections, you can use an existing one or create your own.

### Get an Item or Collection ID

Browse to the item or collection and look at the URL; it contains the ID number. In the example below the ID is `3075706807`.

```
https://steamcommunity.com/sharedfiles/filedetails/?id=3075706807
```

### Create a Collection

A collection is a great way to manage and group all the content you want on your game server.

Go to the collections section of your game's Workshop and select `Create Collection`.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Fill out the form.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Add items to the collection, publish it, then get the collection ID from the page URL. In the example below the collection ID is `157384458`.

```
https://steamcommunity.com/sharedfiles/filedetails/?id=157384458
```

## Steam Web API Key

Some game servers, such as Counter-Strike 2 and Counter-Strike: Global Offensive, need a Steam Web API key (`wsapikey` in the LinuxGSM config) to download Workshop collections. To get a key, visit the [Steam API key page](https://steamcommunity.com/dev/apikey) and follow the instructions.

{% hint style="danger" %}
Do not share your private API key.
{% endhint %}

LinuxGSM Workshop downloads do not need an API key.

## LinuxGSM Workshop Downloads

For game servers that cannot download Workshop content themselves, LinuxGSM downloads and installs it for you. This is available from v26.4.0 for Arma 3, Barotrauma, Colony Survival, DayZ, Left 4 Dead 2, Operation: Harsh Doorstop, Squad, Squad 44, Starbound and Stationeers.

### Setup

Add Workshop item and/or collection IDs to `workshopmods` in the [LinuxGSM config](../configuration/linuxgsm-config.md), separated by spaces.

```bash
workshopmods="450814997 1234567890"
```

Then install them with [workshop-update](../commands/workshop-update.md).

```
./gameserver workshop-update
```

[update](../commands/update.md) also keeps Workshop mods up to date, so a scheduled update covers them too.

### Steam Account Requirements

Whether you need a Steam account that owns the game depends on the game.

| Game server | Server download | Workshop download |
| --- | --- | --- |
| Arma 3 | Any Steam account (not anonymous) | Account must **own Arma 3** |
| Barotrauma | Anonymous | Anonymous |
| Colony Survival | Anonymous | Account must **own Colony Survival** |
| DayZ | Any Steam account (not anonymous) | Account must **own DayZ** |
| Left 4 Dead 2 | Anonymous | Anonymous |
| Operation: Harsh Doorstop | Anonymous | Anonymous |
| Squad | Anonymous | Anonymous |
| Squad 44 | Anonymous | Anonymous |
| Starbound | Account must own Starbound | Uses the same account |
| Stationeers | Anonymous | Anonymous |

Steam only downloads Arma 3, Colony Survival and DayZ Workshop items for an account that owns the game itself, even though their dedicated servers download with any account. If the account in `steamuser` does not own the game, the server installs and runs, but every Workshop item fails to download with `Failure`. Set `steamuser` and `steampass` in the LinuxGSM config, see [SteamCMD Login](README.md#steamcmd-login).

### Where Mods Are Installed

| Game server | Installed to | Loaded by |
| --- | --- | --- |
| Arma 3, DayZ | `serverfiles/workshop/@<id>` | LinuxGSM adds them to `-mod=` on start, in the order listed, after any mods you set in `mods` |
| Barotrauma | `LocalMods/<id>` | LinuxGSM adds each mod to `<regularpackages>` in `config_player.xml`, in the order listed |
| Colony Survival | `gamedata/mods/<id>` | LinuxGSM enables each mod in every world's `gamedata/savegames/<world>/worldconfig.json` |
| Left 4 Dead 2 | `serverfiles/workshop/@<id>`, linked into `left4dead2/addons/<id>.vpk` | The server loads every `.vpk` in `left4dead2/addons` |
| Operation: Harsh Doorstop | `HarshDoorstop/Mods/<mod name>` | The server loads every mod in this folder. Select mod maps and modes with `defaultmap` or `startparameters` |
| Squad | `SquadGame/Plugins/Mods/<id>` | The server loads every mod in this folder |
| Squad 44 | `PostScriptum/Plugins/Mods/<id>` | The server loads every mod in this folder |
| Starbound | `serverfiles/workshop/@<id>`, linked into `serverfiles/mods` | The server loads every `.pak` in `serverfiles/mods` |
| Stationeers | `mods/<id>` | The server enables every mod in this folder in `modconfig.xml` |

For example, on Arma 3:

```
-mod=mods/@mymod\;workshop/@450814997\;workshop/@1234567890
```

### How It Works

* **Collections** are expanded into their items, in the collection's order. Duplicate items are only installed once.
* **Updates:** only new or changed items are downloaded. Downloads happen while the server keeps running, and the server is only restarted if a mod was installed, updated or removed.
* **Arma 3 and DayZ:** file names are converted to lowercase, which these games require on Linux, and each mod's `.bikey` files are copied into `serverfiles/keys`.
* **Removal:** removing an ID from `workshopmods` removes that mod, and its keys, links or config entries, on the next `workshop-update`.
* **Your own mods are kept:** mods and config entries you add yourself are never changed or removed.
* [check-update](../commands/check-update.md) reports Workshop updates without applying them.

{% hint style="info" %}
If you change `workshopmods`, run `workshop-update` before starting the server. LinuxGSM warns on start if a listed mod is not installed yet.
{% endhint %}

{% hint style="warning" %}
Squad 44 on Linux only loads mods whose authors include a Linux server build (`LinuxNoEditor`). Windows-only mods download and install, but the server logs them as invalid and does not load them. Check with the mod author if a mod does not load.
{% endhint %}
