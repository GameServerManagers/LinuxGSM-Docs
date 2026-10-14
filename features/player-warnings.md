# Player Warnings

LinuxGSM can warn players in-game before it stops, restarts or updates a server, so they have time to finish what they are doing.

```
Server restarting in 15 minutes
Server restarting in 10 minutes
Server restarting in 5 minutes
Server restarting in 3 minutes
Server restarting in 1 minute
```

## Enabling warnings

Set `warnplayerstimer` to the number of minutes of warning to give, in `common.cfg` or an instance config. It is off (`0`) by default.

```properties
warnplayerstimer="15"
```

LinuxGSM works out the warnings from the timer, counting down through 60, 30, 15, 10, 5, 3 and 1 minutes:

| `warnplayerstimer` | Warnings at (minutes) |
| ------------------ | --------------------- |
| `15`               | 15, 10, 5, 3, 1       |
| `10`               | 10, 5, 3, 1           |
| `5`                | 5, 3, 1               |
| `1`                | 1                     |
| `7`                | 7, 5, 3, 1            |

The command waits for the countdown to finish before stopping the server, so a `restart` with `warnplayerstimer="15"` takes about 15 minutes.

## When players are warned

| Command                                  | Message                   |
| ---------------------------------------- | ------------------------- |
| `stop`                                   | Server stopping in ...    |
| `restart`                                | Server restarting in ...  |
| `backup` (with `stoponbackup="on"`)      | Server restarting in ...  |
| `update` (when an update is found)       | Server updating in ...    |
| `workshop-update` (when mods changed)    | Server updating in ...    |

There are no warnings when:

* `monitor` restarts a crashed server.
* `force-update` or `validate` is used.
* The server is empty. If everyone leaves during the countdown, LinuxGSM stops waiting and carries on straight away.

Checking for players requires [gamedig](../requirements/gamedig.md) and a working query (`querymode` 2 or 3). If the player count can't be checked, LinuxGSM warns anyway.

If the countdown is cancelled with CTRL+c, players are told the stop or restart was cancelled.

## Supported games

Warnings are sent with the game's own chat command, typed into the server console, so they work for game servers with an interactive console:

| Game servers                                                                                         | Chat command          |
| ---------------------------------------------------------------------------------------------------- | --------------------- |
| Source, Source 2 and GoldSrc games, Quake and Call of Duty games, Xonotic, Minecraft, Terraria, Unturned, Barotrauma, Hytale | `say` |
| Project Zomboid                                                                                      | `servermsg`           |
| Don't Starve Together                                                                                | `c_announce`          |
| SCP: Secret Laboratory                                                                               | `/bc`                 |
| Vintage Story                                                                                        | `/announce`           |
| WaterfallMC                                                                                          | `alert`               |
| Factorio                                                                                             | Plain console text    |

For other game servers, warnings are skipped with `Warning players: not supported`.

## Warnings and stop only if empty

[Stop only if empty](../commands/start-stop-restart.md#stop-only-if-empty-optional) (`stoponlyifnoplayers`) and player warnings work together:

| `stoponlyifnoplayers` | Players online | What happens                                                   |
| --------------------- | -------------- | -------------------------------------------------------------- |
| `on`                  | Yes            | The stop, restart or update is postponed until the server is empty. No warnings are needed. |
| `off`                 | Yes            | Players are warned, then the server stops.                     |
| Either                | No             | The server stops straight away.                                |
