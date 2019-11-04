# start-stop-restart

LinuxGSM provides an easy way to start, stop and restart your game server. LinuxGSM knows the location of the server binaries inserts the start parameters to allow the server to start. LinuxGSM will also run various checks to prevent issues and apply any required server fixes to get the game server running.

## Commands

### Starting a server

Will start the server in a [tmux](../requirements/tmux.md) session allowing the server to run in the background.

`./gameserver start`

### Stopping a server

Stop will attempt a [graceful shutdown](../features/stop-mode.md) of a game server. Failing this it will kill the tmux session.

`./gameserver stop`

### Restarting a server

Will simply stop, then the start the server.

`./gameserver restart`

