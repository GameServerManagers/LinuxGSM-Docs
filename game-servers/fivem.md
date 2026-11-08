# FiveM

## Requirements

- A free Cfx.re server license key. Each server needs its own key.
- A copy of GTA V and the FiveM client to join the server.

LinuxGSM downloads the recommended Linux FXServer build from Cfx.re. The base resources come from the Cfx.re server data repository.

## First Start

1. Get a server key from the [Cfx.re portal](https://portal.cfx.re/servers/registration-keys).
2. Set `sv_licenseKey` in `serverfiles/server.cfg` before starting the server. Keep the key private.
3. Start the server with `./fivemserver start`. If the key is missing, LinuxGSM stops and shows the config file and portal link.

LinuxGSM starts FXServer with `+exec server.cfg`, so it runs without txAdmin. Use LinuxGSM to start, stop, monitor, update and back up the server. The txAdmin web panel is not started.

## Server Settings

Stop the server before editing:

```
serverfiles/server.cfg
```

| Setting                                | Description                                                |
| -------------------------------------- | ---------------------------------------------------------- |
| `sv_licenseKey`                        | Required Cfx.re server key.                                |
| `sv_hostname`                          | Server name.                                               |
| `sv_maxclients`                        | Player limit. More than 48 requires OneSync.               |
| `endpoint_add_tcp`, `endpoint_add_udp` | Listening addresses and ports. Use the same port for both. |
| `ensure`                               | Resources to start.                                        |

For additional FXServer start parameters, set `extraparams` in `lgsm/config-lgsm/fivemserver/fivemserver.cfg`. See [start parameters](../configuration/start-parameters.md#extra-parameters).

## Ports

| Description                 | Port    | Protocol    |
| --------------------------- | ------- | ----------- |
| Game and server information | `30120` | TCP and UDP |

Change both `endpoint_add_tcp` and `endpoint_add_udp` in `server.cfg` when changing the port. Open both protocols in your firewall and publish both when using Docker. Give each instance a different port.

## Updates

`./fivemserver update` and `check-update` use Cfx.re's recommended Linux build. LinuxGSM keeps `server.cfg`, `resources/` and `run.sh` when updating FXServer. It fetches the base resources only when `resources/` is missing, so changes you make there remain in place.

## Resources

Put added resources under `serverfiles/resources/` and add an `ensure` line for each one to `server.cfg`. The default resources come from [cfx-server-data](https://github.com/citizenfx/cfx-server-data).

## Stopping

LinuxGSM uses [stop mode](../features/stop-mode.md) 3, which sends `quit` to the FXServer console.

## Files

| Path                     | Contents                         |
| ------------------------ | -------------------------------- |
| `serverfiles/server.cfg` | Server settings and license key. |
| `serverfiles/resources/` | Base and added resources.        |
| `log/console/`           | LinuxGSM console logs.           |

{% hint style="warning" %}
Backups include `server.cfg` and its license key. Keep backup archives private.
{% endhint %}

## Server Resources

- [Cfx.re server setup](https://docs.fivem.net/docs/server-manual/setting-up-a-server-vanilla/)
- [Cfx.re server commands](https://docs.fivem.net/docs/server-manual/server-commands/)
