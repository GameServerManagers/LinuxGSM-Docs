> note: This is a command for servers using [[SteamCMD]] only.

The `force-update` command bypasses the [[update]] check and runs the [[SteamCMD]] update regardless of if there is an update or not. This will run a [[SteamCMD]] update and restart the game server.

Force update is a useful feature for admins that restart there server on a daily with [[cronjobs]]. It allows LinuxGSM to check for updates while restarting the server.

# Commands

Standard: `./gameserver force-update`

Short: `./gameserver fu`

> note: force-update was previously known as `update-restart`,