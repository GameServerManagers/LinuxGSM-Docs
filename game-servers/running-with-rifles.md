# Running With Rifles

## Requirements

* A **Steam account that owns Running With Rifles**. The dedicated server is part of the game (app 270150) and can't be downloaded anonymously. Set `steamuser` and `steampass` as described in [SteamCMD Login](../steamcmd/README.md#steamcmd-login).
* The **WW2 game modes** also need the account to own the matching DLC (see [DLC Game Modes](#dlc-game-modes)).
* At least 1 GB of RAM.
* Tested on Ubuntu 24.04 and 26.04. The server is 32-bit, so LinuxGSM installs the i386 libraries it needs as dependencies.

## Installing

```
./linuxgsm.sh rwrserver
./rwrserver install
./rwrserver start
```

## Server Settings

The server starts into a lobby, then LinuxGSM runs a game mode script on its console. The server name, port, comment, mode and max players are set in that script, in the `start_server` command.

On install, LinuxGSM copies the default invasion script to an instance script you can edit:

```
serverfiles/media/packages/vanilla/scripts/rwrserver.as
```

Restart the server after editing it.

## Game Modes

The game mode is chosen by two settings in your instance config (`lgsm/config-lgsm/rwrserver/rwrserver.cfg`):

| Setting | Default | Description |
| ------- | ------- | ----------- |
| `startpackage` | `media/packages/vanilla` | Package folder containing the game mode. |
| `startscript` | `${selfname}.as` | Start script inside the package's `scripts` folder. |

For example, to run deathmatch:

```
startpackage="media/packages/deathmatch"
startscript="start_deathmatch_server.as"
```

| Mode | `startpackage` | `startscript` | Default port (UDP) |
| ---- | -------------- | ------------- | ------------------ |
| Invasion (default) | `media/packages/vanilla` | `rwrserver.as` | 1240 |
| Invasion rotator | `media/packages/invasion_rotator` | `start_rotator.as` | 1280 |
| Deathmatch | `media/packages/deathmatch` | `start_deathmatch_server.as` | 1238 |
| Minimodes | `media/packages/minimodes` | `start_minimodes.as` | 1238 |
| Classic | `media/packages/classic` | `start_classic.as` | 1238 |

The scripts in other packages aren't copied by LinuxGSM, so they're overwritten by game updates. To keep changes, copy the script to a new file name in the same folder and point `startscript` at the copy.

{% hint style="info" %}
`./rwrserver details` reads the server name, port, mode and max players from the start script. Scripts that build their settings in code, such as the invasion rotator, may not show all of them.
{% endhint %}

## DLC Game Modes

The WW2 game modes need scripts from the Running With Rifles DLC. The base game includes the `pacific` and `edelweiss` maps, but their `scripts` folders only come with the DLC, which SteamCMD only downloads when the Steam account owns it. Without it, these modes fail with `script build failed` in the console.

| `startpackage` | `startscript` | DLC needed |
| -------------- | ------------- | ---------- |
| `media/packages/ww2_invasion` | `start_invasion_pacific.as` | RUNNING WITH RIFLES: PACIFIC (616850) |
| `media/packages/ww2_invasion` | `start_invasion_edelweiss.as` | RUNNING WITH RIFLES: EDELWEISS (1210750) |
| `media/packages/ww2_invasion` | `start_invasion_combined.as`, `start_rotator.as` | PACIFIC and EDELWEISS |
| `media/packages/ww2_combined` | `start_invasion.as`, `start_campaign.as`, `start_quickmatch.as` | EDELWEISS (1210750) |

After buying the DLC on the server's Steam account, run `./rwrserver validate` so SteamCMD downloads it.

## Stopping

LinuxGSM saves player profiles (`save_profiles`) and stops the game (`stop_server`) before closing the server.

## Logs

The server writes `rwr_server.log` to the top of `serverfiles`. LinuxGSM's console log is in `log/console`.
