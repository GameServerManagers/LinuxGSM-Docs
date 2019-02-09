# logging

Logs are an important part of monitoring a server as it allows you to know what has been happening. LinuxGSM has a log directory that allows you to track the gameserver, console and LinuxGSM itself.

If your user is `gameserver`, then LinuxGSM logs are located in the following directory:

`/home/gameserver/log`

This "log" directory contains two other directories:

* `script`, logs LinuxGSM script activity
* `console`, logs gameserver [console](../commands/console.md) output
* `game`, is a redirect to the game server log files if available.

  **Settings**

You can alter these settings to change LinuxGSM behavior:

```bash
logdays="7" # How long logs are kept
consolelogging="on" # Turning this to off will disable console logging
`
```

_Note:_ `logdays="0"` _means logs will be removed if older than 24h._

### Log clearing

LinuxGSM clears outdated logs according to `logdays` variable setting. This will affect `script` and `console` logs, as well as common game logs.

#### Gamelogs management

LinuxGSM also clears logs from common locations to prevent them from using gigabytes of disk space, including:

* `${systemdir}/logs`
* `${systemdir}/*/logs`
* `${systemdir}/addons/sourcemod/logs`
* `${systemdir}/data/darkrp_logs`
* `${systemdir}/data/ulx_logs`

_Note:_ `${systemdir}` _designates the location of your game server installation_
