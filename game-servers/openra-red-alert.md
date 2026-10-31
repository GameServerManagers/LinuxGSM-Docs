# OpenRA: Red Alert

## Requirements

OpenRA isn't on Steam. LinuxGSM downloads the official Red Alert AppImage from the latest stable [OpenRA release](https://github.com/OpenRA/OpenRA/releases) and extracts it, so FUSE isn't needed. OpenRA only publishes x86_64 Linux builds.

## Client Version

{% hint style="warning" %}
Players can only join a server running the same OpenRA release as their game. After a new OpenRA release, run `./orarserver update` so updated players can join.
{% endhint %}

## Server Settings

OpenRA has no server config file. Settings are start parameters in your LinuxGSM [instance config](../configuration/linuxgsm-config.md). For settings LinuxGSM doesn't list, use `extraparams`, for example `extraparams="Server.RequireAuthentication=True"`. See the OpenRA [Dedicated Server](https://github.com/OpenRA/OpenRA/wiki/Dedicated-Server) wiki for the full list.

## Server Data

Each instance keeps its maps, replays and logs in `serverfiles/data/<instance>`. Updates replace `serverfiles/openra`, so don't put your own files there.
