# OpenRA: Red Alert

## Requirements

- An **x86\_64** Linux server. OpenRA only publishes x86\_64 Linux packages, and LinuxGSM stops with an error on other architectures.
- No Steam account. OpenRA isn't on SteamCMD. LinuxGSM downloads the official Red Alert AppImage from the latest stable [OpenRA GitHub release](https://github.com/OpenRA/OpenRA/releases).

LinuxGSM extracts the AppImage instead of running it, so the server doesn't need FUSE.

## Installing

```
./linuxgsm.sh orarserver
./orarserver install
./orarserver start
```

## Ports

- Game Port Default: 1234 TCP

OpenRA uses a single TCP port. LinuxGSM monitors the server by connecting to it. To run more than one instance, give each one a different `port`.

## Server Settings

OpenRA has no server config file. All settings are start parameters, set in your LinuxGSM [instance config](../configuration/linuxgsm-config.md).

| Setting                   | Default    | Description                                          |
| ------------------------- | ---------- | ---------------------------------------------------- |
| `servername`              | `LinuxGSM` | Name shown in the server browser.                    |
| `serverpassword`          | empty      | Password to join. Empty for none.                    |
| `port`                    | `1234`     | TCP game port.                                       |
| `advertiseonline`         | `True`     | List the server in the public OpenRA server browser. |
| `advertiseonlocalnetwork` | `True`     | Announce the server on the local network.            |
| `enablesingleplayer`      | `True`     | Allow a match to start with a single player.         |
| `recordreplays`           | `False`    | Save replays of matches played on the server.        |

Any other OpenRA server setting can be added with `extraparams`, for example:

```
extraparams="Server.RequireAuthentication=True"
```

See the OpenRA [Dedicated Server](https://github.com/OpenRA/OpenRA/wiki/Dedicated-Server) wiki page for the full list.

## Files

| Path                               | Contents                                                                  |
| ---------------------------------- | ------------------------------------------------------------------------- |
| `serverfiles/openra`               | The extracted OpenRA engine. Replaced on every update.                    |
| `serverfiles/data/<instance>`      | Per-instance data (OpenRA support directory): settings, maps and replays. |
| `serverfiles/data/<instance>/Logs` | OpenRA server logs.                                                       |

Keep your own files in the instance data directory, not in `serverfiles/openra`, because updates replace the engine directory.

## Updating

`./orarserver update` checks the latest stable OpenRA release on GitHub. When a newer release is available, LinuxGSM downloads and extracts it, checks that the server files are complete, then swaps it in for the old engine. If the swap fails, the previous engine is put back. Instance data isn't touched.

{% hint style="warning" %}
Players can only join a server running the same OpenRA release as their game. After a new OpenRA release, players who have updated can't join until the server is updated too, and players who haven't can't join an updated server.
{% endhint %}

Only stable releases are used. Playtest and development builds aren't supported.

## Server Resources

- [OpenRA Dedicated Server wiki](https://github.com/OpenRA/OpenRA/wiki/Dedicated-Server)
- [OpenRA AppImages wiki](https://github.com/OpenRA/OpenRA/wiki/AppImages)
