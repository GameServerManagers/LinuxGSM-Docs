# Counter-Strike: WON2

Counter-Strike: WON2 (`cswonserver`) runs Counter-Strike 1.5 on the native Linux Half-Life dedicated server 3.1.1.1 (engine 1.1.1.0, protocol 46). This is the last version of Counter-Strike from before it moved to Steam. Community WON2 master servers keep the server browser working.

For the Steam version of Counter-Strike, use [Counter-Strike 1.6](https://linuxgsm.com/servers/csserver/) (`csserver`) instead.

## Requirements

* Players need the retail (pre-Steam) Half-Life client patched to version 1.1.1.0, the Counter-Strike 1.5 client and the WON2 player patch. The Steam version of Counter-Strike uses protocol 48 and can't connect.
* The server is 32-bit. LinuxGSM installs the 32-bit libraries it needs during install.

## Installation

LinuxGSM downloads a single archive from linuxgsm.download. It contains:

* Half-Life dedicated server 3.1.1.1 with the 3.1.1.1e update.
* The Counter-Strike 1.5 server files from Valve, in the `cstrike` folder.
* The WON2 `hlds_run` launcher and the community protection libraries (`nowon.so`, `hlds_20040707fix.so` and `hlshield.so`).
* The WON2 master server list (`valve/valvecomm.lst`).

The archive contains Valve files only, with no Metamod or other add-ons. The server doesn't use SteamCMD and its version is fixed, so the `update`, `check-update` and `validate` commands aren't available.

## Server Settings

The port, map and max players are set in your instance config (`lgsm/config-lgsm/cswonserver/cswonserver.cfg`):

| Setting | Default |
| ------- | ------- |
| `port` | `27015` |
| `clientport` | `27005` |
| `defaultmap` | `de_dust2` |
| `maxplayers` | `16` |

Other settings, including `hostname`, `rcon_password`, `sv_password` and the Counter-Strike game rules (`mp_friendlyfire`, `mp_roundtime` and so on), are in the server config:

```
serverfiles/cstrike/cswonserver.cfg
```

## Ports

| Port | Protocol | Default | Description |
| ---- | -------- | ------- | ----------- |
| Game | UDP | 27015 | Set by `port`. |
| Query | UDP | 27015 | The same port as the game. |
| Client | UDP | 27005 | Set by `clientport`. |

## Connecting

Players can join from the in-game console:

```
connect <server-ip>:27015
```

The server also lists itself on the WON2 master servers in `valve/valvecomm.lst`, which the server browser in a WON2-patched client uses.

## Security

{% hint style="warning" %}
The Half-Life 1.1.1.0 engine is over 20 years old and no longer maintained. The community protection libraries fix some known exploits, but they don't make the server fully secure. The server runs with `-insecure`, so there is no Valve anti-cheat.
{% endhint %}

## Unavailable Commands

* `update`, `check-update` and `validate`: there are no updates for this server.
* `fastdl`: protocol 46 clients predate HTTP downloads (`sv_downloadurl`), so custom content downloads from the game server itself.

## Stopping

LinuxGSM uses [stop mode](../features/stop-mode.md) 9 (GoldSrc), which sends `quit` to the server console.

## Logs

The server writes its logs to `serverfiles/cstrike/logs`.
