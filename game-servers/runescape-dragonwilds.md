# RuneScape: Dragonwilds

## Server Resources

* [RuneScape: Dragonwilds Dedicated Servers (wiki)](https://dragonwilds.runescape.wiki/w/Dedicated\_Servers)

The dedicated server is a native Linux build, downloaded with SteamCMD (App ID `4019830`, about 5 GB). LinuxGSM recommends at least 2 GB of RAM.

## First Start: Set the Owner ID

{% hint style="warning" %}
The server will not finish starting until `OwnerId` is set. The server console shows: "The \[OwnerId] for this server is empty. An OwnerId is required for normal Server operation."
{% endhint %}

Most server settings live in `DedicatedServer.ini`, which the server creates the first time it starts:

```
serverfiles/RSDragonwilds/Saved/Config/LinuxServer/DedicatedServer.ini
```

1. Install and start the server once so that `DedicatedServer.ini` is created:

   ```
   ./rsdwserver install
   ./rsdwserver start
   ./rsdwserver stop
   ```

2. Find your Player ID in the game's settings menu and set it as `OwnerId` in `DedicatedServer.ini`:

   ```ini
   [/Script/Dominion.DedicatedServerSettings]
   OwnerId=YOUR_PLAYER_ID
   ServerName=My Dragonwilds Server
   WorldPassword=
   DefaultWorldName=World-12345
   ```

3. Start the server again:

   ```
   ./rsdwserver start
   ```

## Server Settings

These settings are read from `DedicatedServer.ini`, not from LinuxGSM config. Stop the server before editing.

| Setting            | Description                                    |
| ------------------ | ---------------------------------------------- |
| `OwnerId`          | Your Player ID. Required.                      |
| `ServerName`       | Name shown to players.                         |
| `WorldPassword`    | Password players need to join. Leave empty for none. |
| `AdminPassword`    | Password for admin access.                     |
| `DefaultWorldName` | The world the server loads.                    |

`./rsdwserver details` shows the server name, world name and Owner ID that LinuxGSM reads from this file.

## Ports

| Description | Port   | Protocol |
| ----------- | ------ | -------- |
| Game        | `7777` | UDP      |

To change the port, set `port` in your LinuxGSM instance config (`lgsm/config-lgsm/rsdwserver/rsdwserver.cfg`). It is passed to the server as `-Port=`. Players can join with **Direct Connect** using your server's IP and port.
