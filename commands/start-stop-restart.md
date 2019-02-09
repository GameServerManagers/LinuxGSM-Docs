# start-stop-restart

LinuxGSM provides an easy way to start, stop and restart your game server. LinuxGSM knows the location of the server binaries inserts the start parameters to allow the server to start. LinuxGSM will also run various checks to prevent issues and apply any required server fixes to get the game server running.

## Commands

### Starting a server

Will start the server in a tmux session allowing the server to run in the background.

`./gameserver start`

### Stopping a server

Stop will do a graceful shutdown \(sends "quit" command to Source servers for example\) of a server when possible. Failing this it will force stop.

`./gameserver stop`

### Restarting a server

Will simply stop, then the start the server.

`./gameserver restart`
