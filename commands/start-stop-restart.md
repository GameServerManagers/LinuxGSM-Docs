# start-stop-restart

LinuxGSM provides an easy way to start, stop and restart your game server. LinuxGSM knows the location of the server binaries and inserts the start parameters to allow the server to start. LinuxGSM will also run various checks to prevent issues and apply any required server fixes to get the game server running.

## Commands

### Starting a server

Will start the server in a [tmux](../requirements/tmux.md) session allowing the server to run in the background.

`./gameserver start`

### Stopping a server

Stop will attempt a [graceful shutdown](../features/stop-mode.md) of a game server. Failing this stop will kill the tmux session.

`./gameserver stop`

#### Stop only if empty (optional)

If the `stoponlyifnoplayers` setting is enabled, LinuxGSM will only stop the server when it is empty and prevent it from stopping otherwise.

{% hint style="warning" %}
This feature requires [gamedig](../requirements/gamedig.md) (which needs Node.js 16 or newer) and a working query (`querymode` 2 or 3). If the player count can't be checked, LinuxGSM shows `Unable to determine player count` with the reason and stops the server anyway.
{% endhint %}

```properties
stoponlyifnoplayers="off"
```

When a `restart` is requested while players are online, the restart is **postponed** rather than cancelled: LinuxGSM records a restart request and the [monitor](monitor.md) command will retry the restart automatically once the server is empty. Enable a monitor cronjob for postponed restarts to be carried out.

An `update` that finds an update while players are online is postponed in the same way, and the monitor command applies it once the server is empty.

By default this protection applies to **all** commands that stop the server, including `update`. To limit it to only the explicit `stop` and `restart` commands (so an `update` can still stop the server even while players are online), set `stoponlyifnoplayersallcommands` to `off`.

```properties
# Apply "stop only if empty" to every command that stops the server (default).
stoponlyifnoplayersallcommands="on"
# Or limit it to explicit stop/restart only:
# stoponlyifnoplayersallcommands="off"
```

#### Warn players before stopping (optional)

LinuxGSM can count down with in-game messages before it stops, restarts or updates the server. See [Player Warnings](../features/player-warnings.md).

```properties
warnplayerstimer="15"
```

### Restarting a server

Will simply stop, and then start the server.

`./gameserver restart`
