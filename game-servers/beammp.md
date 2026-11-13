# BeamMP

## Requirements

- A **BeamMP AuthKey** from [keymaster.beammp.com](https://keymaster.beammp.com). The server won't run without one.
- **Debian or Ubuntu**. BeamMP only publishes Linux builds for these. RHEL, Rocky Linux, AlmaLinux and CentOS Stream 10 or newer use the Ubuntu 24.04 build, which needs glibc 2.38. On other distros, including version 9 of those, the install stops with an error.
- x86\_64 or arm64.
- Players need BeamNG.drive with the BeamMP mod.

LinuxGSM downloads the server from the [BeamMP-Server releases](https://github.com/BeamMP/BeamMP-Server/releases) on GitHub.

## First Start

1. Run `./bmpserver install`.
2. Set `AuthKey` in `serverfiles/bmpserver.toml`.
3. Run `./bmpserver start`.

Until an AuthKey is set, `start` stops with a message instead of launching the server.

## Server Settings

The server settings are in the BeamMP config file:

```
serverfiles/bmpserver.toml
```

Stop the server before editing it. Common settings:

| Setting       | Default                        | Description                                                                            |
| ------------- | ------------------------------ | -------------------------------------------------------------------------------------- |
| `AuthKey`     | empty                          | Key from keymaster.beammp.com. Required.                                               |
| `Name`        | `LinuxGSM`                     | Server name.                                                                           |
| `Description` | `BeamMP Default Description`   | Server description.                                                                    |
| `MaxPlayers`  | `8`                            | Maximum players.                                                                       |
| `MaxCars`     | `1`                            | Maximum cars per player.                                                               |
| `Map`         | `/levels/gridmap_v2/info.json` | Map to load.                                                                           |
| `Private`     | `true`                         | When `true`, the server isn't listed in the public server list. Players connect by IP. |
| `AllowGuests` | `true`                         | Allow players without a BeamMP account.                                                |

The port and start parameters are in your instance config (`lgsm/config-lgsm/bmpserver/bmpserver.cfg`). LinuxGSM passes `port` to the server as `--port`, which overrides `Port` in `bmpserver.toml`.

| Setting       | Default   | Description                                                                                                                                       |
| ------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ip`          | `0.0.0.0` | IP address shown by `details`.                                                                                                                    |
| `port`        | `30814`   | Game port.                                                                                                                                        |
| `extraparams` | empty     | Extra start parameters, added to the end of the command. See the [BeamMP-Server README](https://github.com/BeamMP/BeamMP-Server) for the options. |

## Ports

| Description | Port    | Protocol    |
| ----------- | ------- | ----------- |
| Game        | `30814` | TCP and UDP |

To change the port, set `port` in your instance config. Open both TCP and UDP on your firewall. Give each instance on the same machine its own port.

## Updates

`./bmpserver update` installs the latest release. LinuxGSM picks the build for your distro and CPU, using the newest build that isn't newer than your distro (Ubuntu 26.04 uses the Ubuntu 24.04 build), and checks the SHA256 checksum before installing.

{% hint style="warning" %}
Players need a BeamMP client that matches the server version. Check the [release notes](https://github.com/BeamMP/BeamMP-Server/releases) before updating a public server.
{% endhint %}

## Mods

Client mods and server plugins go in the `Resources` folder in `serverfiles`. See the [BeamMP documentation](https://docs.beammp.com/server/) for the layout.

## Stopping

BeamMP stops with CTRL+c. See [Stop Mode](../features/stop-mode.md).

## Server Resources

- [BeamMP](https://beammp.com/)
- [BeamMP server documentation](https://docs.beammp.com/server/)
- [BeamMP wiki: server installation](https://wiki.beammp.com/en/home/server-installation)
- [BeamMP-Server on GitHub](https://github.com/BeamMP/BeamMP-Server)
