LGSM provides an easy way to start, stop, or restart your game server.

_Of course, install your server with the [[Installer]] first._

## Starting a server

`./gameserver start`

Will start the server in a tmux occurrence. 

### Stopping a server

`./gameserver stop`

Will stop a server with a proper way, and force close it after 30s if it doesn't close properly (graceful shutdown).

## Restarting a server

`./gameserver restart`

Will use the stop, then the start functions.