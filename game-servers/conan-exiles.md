# Conan Exiles

## Requirements

- glibc 2.28 or newer. The native Linux server arrived with the Conan Exiles Enhanced update.
- At least 8 GB of RAM.

The dedicated server (Steam app 443030) downloads anonymously, so no Steam login is needed.

## Server Settings

The server name, max players and ports are set as start parameters in your instance config (`lgsm/config-lgsm/ceserver/ceserver.cfg`):

| Setting      | Default    |
| ------------ | ---------- |
| `servername` | `LinuxGSM` |
| `maxplayers` | `40`       |
| `port`       | `7777`     |
| `queryport`  | `27015`    |

Other settings are in `ServerSettings.ini`, which the server creates on its first start:

```
serverfiles/ConanSandbox/Saved/Config/LinuxServer/ServerSettings.ini
```

This includes `AdminPassword` and `ServerPassword`. Stop the server before editing it, then start it again.

## Ports

| Description | Port    | Protocol |
| ----------- | ------- | -------- |
| Game        | `7777`  | UDP      |
| Raw UDP     | `7778`  | UDP      |
| Query       | `27015` | UDP      |

The game port is set by `port` and the query port by `queryport`. The raw UDP port is always `port` + 1.

When running more than one instance, leave a gap of at least two between game ports, so the raw port doesn't clash.

## RCON

RCON is off by default. To enable it, add an `[RconPlugin]` section to `Game.ini` in the same folder as `ServerSettings.ini`:

```
[RconPlugin]
RconEnabled=1
RconPassword=CHANGEME
RconPort=25575
```

If you enable RCON, also open the RCON port (TCP) in your firewall.

## Stopping

The Conan Exiles server doesn't exit after a single CTRL+c, so LinuxGSM uses [stop mode](../features/stop-mode.md) 16, which sends CTRL+c twice.

## Logs

The server writes its logs to `serverfiles/ConanSandbox/Saved/Logs`.
