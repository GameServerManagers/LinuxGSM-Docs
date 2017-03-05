LinuxGSM provides an easy way to start, stop, or restart your game server.

## Starting a server

`./gameserver start`

Will start the server in a tmux occurrence. 

### Stopping a server

`./gameserver stop`

Will attempt to correctly stop a server using (graceful shutdown). Should this fail it will be forced to stop after 30 seconds.

## Restarting a server

`./gameserver restart`

Will use the stop, then the start the server.