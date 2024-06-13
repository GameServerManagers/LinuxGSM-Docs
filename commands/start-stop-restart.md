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

If `stoponlyifnoplayers` setting is enabled LinuxGSM will only stop the server if it is empty and prevent it from stopping otherwise. This feature only works with game servers that can use gamedig.

```properties
stoponlyifnoplayers="off"
```

### Restarting a server

Will simply stop, and then start the server.

`./gameserver restart`
