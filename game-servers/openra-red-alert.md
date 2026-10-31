# OpenRA: Red Alert

## Requirements

- An x86\_64 server. OpenRA only publishes x86\_64 Linux builds.

OpenRA isn't on Steam. LinuxGSM downloads the official Red Alert AppImage from the latest stable [OpenRA release](https://github.com/OpenRA/OpenRA/releases) and extracts it, so FUSE isn't needed.

## Server Settings

OpenRA has no server config file. All settings are start parameters in your LinuxGSM instance config (`lgsm/config-lgsm/orarserver/orarserver.cfg`):

| Setting                   | Default    | Description                                          |
| ------------------------- | ---------- | ---------------------------------------------------- |
| `servername`              | `LinuxGSM` | Name shown in the server browser.                    |
| `serverpassword`          | empty      | Password to join. Empty for none.                    |
| `advertiseonline`         | `True`     | List the server in the public OpenRA server browser. |
| `advertiseonlocalnetwork` | `True`     | Announce the server on the local network.            |
| `enablesingleplayer`      | `True`     | Allow a match to start with one player.              |
| `recordreplays`           | `False`    | Save replays of matches played on the server.        |

For any other OpenRA server setting, use `extraparams`, for example `extraparams="Server.RequireAuthentication=True"`. The [Dedicated Server](https://github.com/OpenRA/OpenRA/wiki/Dedicated-Server) wiki page lists them.

## Ports

| Description | Port   | Protocol |
| ----------- | ------ | -------- |
| Game        | `1234` | TCP      |

To change the port, set `port` in your instance config. LinuxGSM monitors the server by connecting to this port. When running more than one instance, give each one a different port.

## Updates

`./orarserver update` installs the latest stable OpenRA release. Playtest and development builds aren't used. LinuxGSM checks the new release is complete before swapping it in, and puts the previous release back if the swap fails.

{% hint style="warning" %}
Players can only join a server running the same OpenRA release as their game. After a new OpenRA release, update the server so updated players can join.
{% endhint %}

## Files

| Path                               | Contents                                              |
| ---------------------------------- | ----------------------------------------------------- |
| `serverfiles/openra`               | The OpenRA engine. Replaced on every update.          |
| `serverfiles/data/<instance>`      | Per-instance data: OpenRA settings, maps and replays. |
| `serverfiles/data/<instance>/Logs` | Server logs.                                          |

Keep your own files in the instance data directory, not in `serverfiles/openra`.

## Server Resources

- [OpenRA Dedicated Server wiki](https://github.com/OpenRA/OpenRA/wiki/Dedicated-Server)
- [OpenRA AppImages wiki](https://github.com/OpenRA/OpenRA/wiki/AppImages)
