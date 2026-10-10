# Workshop

Many Steam games support the [Steam Workshop](https://steamcommunity.com/workshop). It is an easy way to share community game modes, maps, skins, and other community-made content.

For game servers, the Workshop allows community content (mainly maps, game modes and mods) to be made available to play on game servers. For most games, players who connect download the content automatically, which removes the need to set up a [FastDL](../commands/fastdl.md) server.

Game servers get Workshop content in one of two ways:

* **The game server downloads it.** You add item or collection IDs to the game server config or start parameters, and the server downloads them when it starts. LinuxGSM adds the settings to the config where they are available.
* **LinuxGSM downloads it.** Some game servers cannot download Workshop content. For these, LinuxGSM downloads the content with SteamCMD, installs it and keeps it up to date using the [workshop-update](../commands/workshop-update.md) command.

## Supported Game Servers

| Game server | Downloaded by | Where to add Workshop content |
| --- | --- | --- |
| ARK: Survival Evolved | Game server | `ActiveMods=` in `GameUserSettings.ini` (`-AutoManagedMods` is in the default start parameters) |
| Arma 3 | LinuxGSM (v26.4.0+) | `workshopmods` in the [LinuxGSM config](../configuration/linuxgsm-config.md), see [below](#linuxgsm-workshop-downloads) |
| Counter-Strike 2 | Game server | `+host_workshop_collection` or `+host_workshop_map` in `startparameters`, with `wsapikey` |
| Counter-Strike: Global Offensive | Game server | `wscollectionid`, `wsstartmap` and `wsapikey` in the LinuxGSM config |
| DayZ | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config, see [below](#linuxgsm-workshop-downloads) |
| Day of Infamy | Game server | `subscribed_file_ids.txt` in the game directory (`-workshop` is in the default start parameters) |
| Don't Starve Together | Game server | `dedicated_server_mods_setup.lua` |
| Garry's Mod | Game server | `wscollectionid` in the LinuxGSM config |
| Insurgency | Game server | `subscribed_file_ids.txt` in the game directory (`-workshop` is in the default start parameters) |
| Killing Floor 2 | Game server | `ServerSubscribedWorkshopItems` in `PCServer-KFEngine.ini` |
| Natural Selection 2 | Game server | `-mods` in `startparameters` (`mods` in the LinuxGSM config for NS2: Combat) |
| Project Zomboid | Game server | `WorkshopItems=` and `Mods=` in the server `.ini` |
| Squad | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config, see [below](#linuxgsm-workshop-downloads) |
| Starbound | LinuxGSM (v26.4.0+) | `workshopmods` in the LinuxGSM config, see [below](#linuxgsm-workshop-downloads) |
| Unturned | Game server | `WorkshopDownloadConfig.json` |

{% hint style="info" %}
Insurgency: Sandstorm uses [mod.io](https://mod.io), not the Steam Workshop.
{% endhint %}

## Steam Web API Key/Auth Key

Some game servers require a Steam API key to access Workshop content. To get this key visit the [Steam API key page](https://steamcommunity.com/dev/apikey) and follow the instructions.

{% hint style="danger" %}
Do not share your private API key.
{% endhint %}

## Items and Collections

The Steam Workshop is made up of individual items such as maps, game modes, skins, etc, and also collections of these items. Game servers can download these items and collections by getting their unique ID number and adding it to the game server config or parameter. For collections, it is possible to find and use an existing one or create your own.

### Get an Item or Collection ID

To get an item or collection ID, browse to the item you want to add and look at the URL; it will contain the required ID number. In the example below the ID is `3075706807`.

```
https://steamcommunity.com/sharedfiles/filedetails/?id=3075706807
```

### Create a Collection

Creating a collection is a great way to manage and group all the content that you want on your game server.&#x20;

To create your collection go to the collections section of your games Workshop, and select `Create Collection`.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Fill out the form.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Add any maps to the collection, then publish the completed collection. Then get the collection ID which can be found on the page URL. The collection ID in the url below is `157384458`.

```
https://steamcommunity.com/sharedfiles/filedetails/?id=157384458
```

## LinuxGSM Workshop Downloads

For game servers that cannot download Workshop content themselves, LinuxGSM downloads and installs it for you. This is available for Arma 3, DayZ, Squad and Starbound from v26.4.0.

### Steam Account Requirements

Whether you need a Steam account that owns the game depends on the game.

| Game server | Server download | Workshop download |
| --- | --- | --- |
| Arma 3 | Any Steam account (not anonymous) | Account must **own Arma 3** |
| DayZ | Any Steam account (not anonymous) | Account must **own DayZ** |
| Squad | Anonymous | Anonymous |
| Starbound | Account must own Starbound | Uses the same account |

For Arma 3 and DayZ, the dedicated server is free with any Steam account, but Steam only downloads Workshop items for an account that owns the game itself. If the account in `steamuser` does not own the game, the server installs and runs, but every Workshop item fails to download with `Failure`. Set `steamuser` and `steampass` in the [LinuxGSM config](../configuration/linuxgsm-config.md), see [SteamCMD login](README.md#steamcmd-login).

### Setup

Add the Workshop item and/or collection IDs to `workshopmods` in the LinuxGSM config, separated by spaces.

```bash
workshopmods="450814997 1234567890"
```

Then install them.

```
./arma3server workshop-update
```

Where each game's mods are installed, and how they are loaded:

| Game server | Installed to | Loaded by |
| --- | --- | --- |
| Arma 3, DayZ | `serverfiles/workshop/@<id>` | LinuxGSM adds them to `-mod=` on start, in the order listed, after any mods you set in `mods` |
| Squad | `SquadGame/Plugins/Mods/<id>` | The server loads every mod in this folder |
| Starbound | `serverfiles/workshop/@<id>`, linked into `serverfiles/mods` | The server loads every `.pak` in `serverfiles/mods` |

For example, on Arma 3:

```
-mod=mods/@mymod\;workshop/@450814997\;workshop/@1234567890
```

### How it works

* **Collections** are expanded into their items, in the collection's order. Duplicate items are only installed once.
* **Updates:** only new or changed items are downloaded. The download happens while the server is running, and the server is only restarted if a mod was installed, updated or removed.
* **Install:** for Arma 3 and DayZ, file names are converted to lowercase, which these games require on Linux, and each mod's `.bikey` files are copied into `serverfiles/keys`.
* **Removal:** removing an ID from `workshopmods` removes that mod (and its keys or links) on the next `workshop-update`. Mods you added yourself are never removed.
* [update](../commands/update.md) also updates Workshop mods, and [check-update](../commands/check-update.md) reports Workshop updates without applying them.

{% hint style="info" %}
If you change `workshopmods`, run `workshop-update` before starting the server. LinuxGSM will warn on start if a listed mod is not installed yet.
{% endhint %}
