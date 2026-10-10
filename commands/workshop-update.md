# workshop-update

Installs, updates and removes the Steam Workshop mods set in `workshopmods`, for game servers that cannot download Workshop content themselves.

Available for Arma 3, DayZ, Squad and Starbound from v26.4.0. See [Workshop](../steamcmd/workshop.md#linuxgsm-workshop-downloads) for setup and requirements.

{% hint style="warning" %}
For Arma 3 and DayZ, the Steam account in `steamuser` must own the game, not just the dedicated server. Otherwise every Workshop item fails to download. Squad and Starbound Workshop items download without this.
{% endhint %}

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
* Installs each item where the game loads mods from. For Arma 3 and DayZ, it also converts file names to lowercase and copies keys into `serverfiles/keys`.
* Removes mods that are no longer in `workshopmods`. Mods you added yourself are left alone.
* If the server is running and anything was installed, updated or removed, the server is restarted.

The [update](update.md) command runs the same Workshop update after updating the game server.
