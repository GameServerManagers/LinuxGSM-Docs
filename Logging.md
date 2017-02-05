# LGSM Logs

If your user is "gameserver", then LGSM logs are located in the following directory:

`/home/gameserver/log`  

This "log" directory contains two other directories:  
* `script`, logs LGSM script activity
* `console`, logs gameserver [console](https://github.com/GameServerManagers/LinuxGSM/wiki/Console) output

# Settings

You can alter these settings to change LGSM's behavior:  

```bash
logdays="7" # How long logs are kept
consolelogging="on" # Turning this to off will disable console logging
````

_Note: `logdays="0"` means logs will be removed if older than 24h._

## Log clearing
LGSM clears outdated logs according to `logdays` variable setting. This will affect `script` and `console` logs, as well as common game logs.


### Gamelogs management

LGSM also clears logs from common locations to prevent them from using gigabytes of disk space, including:  
* `${systemdir}/logs`
* `${systemdir}/*/logs`
* `${systemdir}/addons/sourcemod/logs`
* `${systemdir}/data/darkrp_logs `
* `${systemdir}/data/ulx_logs`

_Note: `${systemdir}` designates the location of your game server installation_