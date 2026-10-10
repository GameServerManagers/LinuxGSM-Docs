# workshop-update

Installs, updates and removes the Steam Workshop mods set in `workshopmods`, for game servers that cannot download Workshop content themselves.

Available for Arma 3 and DayZ from v26.4.0. See [Workshop](../steamcmd/workshop.md#linuxgsm-workshop-downloads) for setup and requirements.

## Usage

```
./gameserver workshop-update
```

```
./gameserver wu
```

## What it does

* Expands any collections in `workshopmods` and checks each item for updates.
* Downloads new and changed items with SteamCMD while the server keeps running.
* Installs each item to `serverfiles/workshop/@<id>`, converts its file names to lowercase and copies its keys into `serverfiles/keys`.
* Removes mods that are no longer in `workshopmods`.
* If the server is running and anything was installed, updated or removed, the server is restarted.

The [update](update.md) command runs the same Workshop update after updating the game server.
