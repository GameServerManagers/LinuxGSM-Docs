# Battlefront Eternal

## Requirements

- A Steam account that owns STAR WARS Battlefront (Classic, 2004). Set `steamuser` and `steampass` in your LinuxGSM instance config. Anonymous SteamCMD download does not work.
- At least 2 GB of RAM. The retail game download is about 2.8 GB, and prepared data uses about 2.2 GB more.
- glibc 2.28 or newer.

LinuxGSM downloads the native Battlefront Eternal server and Node.js 24, then prepares server data from your owned retail game files. Battlefront Eternal is still in development preview.

## First Start

1. Set the Steam account in `lgsm/config-lgsm/bfeserver/bfeserver.cfg`, then install the server. LinuxGSM downloads and prepares the game data.
2. Edit `serverfiles/bfe-state/config.json` to set the server name, ports, player limit and map rotation.
3. To list the server publicly, read the project's online notice and set `"onlineNoticeAccepted": true` in `config.json`. The default is `false`, so the server is limited to LAN or direct connection until you accept it.

## Server Settings

Stop the server before editing:

```
serverfiles/bfe-state/config.json
```

| Setting                | Default      | Description                                                       |
| ---------------------- | ------------ | ----------------------------------------------------------------- |
| `name`                 | `SERVERNAME` | Name shown to players.                                            |
| `gamePort`             | `18451`      | Game UDP port and HTTP server information port.                   |
| `discoveryPort`        | `18452`      | LAN discovery port.                                               |
| `maxPlayers`           | `64`         | Player limit.                                                     |
| `rotation`             | Six maps     | Maps and modes played in order.                                   |
| `onlineNoticeAccepted` | `false`      | Set to `true` after accepting the online notice to list publicly. |

The LinuxGSM instance setting `healthport="18450"` controls the local health and admin endpoint. Each instance on the same host needs a different health port as well as different game and discovery ports. Additional start parameters can go in `extraparams`. See [start parameters](../configuration/start-parameters.md#extra-parameters).

## Ports

| Description                           | Port    | Protocol        |
| ------------------------------------- | ------- | --------------- |
| Local health and admin                | `18450` | TCP, local only |
| Game                                  | `18451` | UDP             |
| Server information and LinuxGSM query | `18451` | TCP             |
| LAN discovery                         | `18452` | UDP             |

Change `gamePort` and `discoveryPort` in `config.json`, and `healthport` in the LinuxGSM instance config. Open or publish the game and server information ports for remote players. LinuxGSM checks the TCP server information port when monitoring.

## Updates

`update` and `check-update` check Battlefront Eternal releases and Node.js 24. A Node-only update also restarts the server. `validate` checks the owned retail game files; it does not replace the Battlefront Eternal server, prepared data or Node.js. LinuxGSM prepares game data again when the server release changes the preparation tools.

## Stopping

LinuxGSM uses [stop mode](../features/stop-mode.md) 2, which sends CTRL+c.

## Files

| Path                                | Contents                                           |
| ----------------------------------- | -------------------------------------------------- |
| `serverfiles/GameData/`             | Retail game files downloaded through SteamCMD.     |
| `serverfiles/bfe/`                  | Battlefront Eternal server and preparation tools.  |
| `serverfiles/bfe-data/`             | Prepared game data.                                |
| `serverfiles/bfe-state/`            | Server config, identity, operator token and state. |
| `serverfiles/node/`                 | Node.js runtime.                                   |
| `log/script/<instance>-prepare.log` | Game data preparation log.                         |

{% hint style="warning" %}
`bfe-state/` contains identity and operator credentials. Keep backups private.
{% endhint %}

## Server Resources

- [Battlefront Eternal server guide](https://battlefronteternal.com/servers/)
- [Battlefront Eternal releases](https://get.battlefronteternal.com/downloads/latest)
