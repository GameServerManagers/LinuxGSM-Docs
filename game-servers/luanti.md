# Luanti

Luanti was previously called Minetest.

## Requirements

- An x86\_64 or aarch64 server.

Luanti isn't on Steam. LinuxGSM downloads the portable headless server builds from [rollerozxa/luantiserver](https://github.com/rollerozxa/luantiserver), as recommended by the [Luanti server docs](https://docs.luanti.org/for-server-hosts/setup/linux/), and checks each download's SHA256 checksum. A new install also includes [Minetest Game](https://github.com/luanti-org/minetest_game) 5.8.0 as the default game.

## Server Settings

The instance config (`lgsm/config-lgsm/luantiserver/luantiserver.cfg`) sets the start parameters:

| Setting     | Default    | Description                                                    |
| ----------- | ---------- | -------------------------------------------------------------- |
| `ip`        | `0.0.0.0`  | Address the server binds to.                                   |
| `port`      | `30000`    | UDP game port.                                                 |
| `gameid`    | `minetest` | Game to run. Must match a folder in `serverfiles/games`.       |
| `worldname` | `world`    | World folder in `serverfiles/worlds`. Created if it's missing. |

To run a different game, put it in `serverfiles/games/<gameid>` (for example from [ContentDB](https://content.luanti.org/)), then set `gameid`. To start a new world, set a new `worldname`. A world keeps the game it was created with, so use a new `worldname` when you change `gameid`. Restart the server after changing either.

The game server settings are in:

```
serverfiles/luantiserver.cfg
```

LinuxGSM creates it on install from Luanti's `minetest.conf.example` and adds these settings at the end:

| Setting           | Default    | Description                                                   |
| ----------------- | ---------- | ------------------------------------------------------------- |
| `server_name`     | `LinuxGSM` | Name shown in the server list.                                |
| `name`            | `admin`    | Administrator. The player with this name gets all privileges. |
| `server_announce` | `false`    | Set to `true` to list the server on the public server list.   |
| `bind_address`    | `0.0.0.0`  | Address the server binds to. Taken from `ip` on install.      |
| `max_users`       | `20`       | Maximum number of players.                                    |

Change `name` to your own player name before you first join, so nobody else can claim the administrator account. Stop the server before editing the file, then start it again. `./luantiserver details` shows the server name, password and max players from this file. The full list of settings, with descriptions, is in the rest of the file.

## Ports

| Description | Port    | Protocol |
| ----------- | ------- | -------- |
| Game        | `30000` | UDP      |

To change the port, set `port` in your instance config. It's passed to the server as `--port`. When running more than one instance, give each one a different port.

## Updates

`./luantiserver update` installs the latest release from [rollerozxa/luantiserver](https://github.com/rollerozxa/luantiserver/releases) over the engine files, then checks the server reports the new version. Games, mods, worlds and `luantiserver.cfg` aren't touched, and Minetest Game isn't updated after the first install.

## Files

| Path                               | Contents                          |
| ---------------------------------- | --------------------------------- |
| `serverfiles/luantiserver.cfg`     | Server settings.                  |
| `serverfiles/games`                | Games, including Minetest Game.   |
| `serverfiles/mods`                 | Mods shared by all worlds.        |
| `serverfiles/worlds/<worldname>`   | World data, including `world.mt`. |
| `log/server/luantiserver-game.log` | Server log.                       |

## Server Resources

- [Luanti server hosting docs](https://docs.luanti.org/for-server-hosts/setup/linux/)
- [ContentDB](https://content.luanti.org/) (games, mods and texture packs)
- [Luanti settings reference (minetest.conf.example)](https://github.com/luanti-org/luanti/blob/master/minetest.conf.example)
