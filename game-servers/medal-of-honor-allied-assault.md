# Medal of Honor: Allied Assault

## Requirements

- The vanilla and Reborn variants are 32-bit and need i386 libraries, which the LinuxGSM dependency check installs. LinuxGSM also installs the old `libstdc++5` they need into `serverfiles` on start.
- The OpenMoHAA variants need a 64-bit (x86_64) system.

LinuxGSM downloads the server files and the game data for Allied Assault, Spearhead and Breakthrough from linuxgsm.download. OpenMoHAA is downloaded from its GitHub release when an OpenMoHAA variant is first used.

## Variants

One `mohaaserver` runs Allied Assault and both expansions, Spearhead and Breakthrough. The `variant` setting picks the game and the server build:

| Variant                   | Game           | Server build                                    |
| ------------------------- | -------------- | ----------------------------------------------- |
| `alliedassault-reborn`    | Allied Assault | Original 1.11 engine with the Reborn 1.12 patch |
| `alliedassault-vanilla`   | Allied Assault | Original 1.11 engine and game module            |
| `alliedassault-openmohaa` | Allied Assault | OpenMoHAA                                       |
| `spearhead-vanilla`       | Spearhead      | Original 2.15 engine and game module            |
| `spearhead-openmohaa`     | Spearhead      | OpenMoHAA                                       |
| `breakthrough-openmohaa`  | Breakthrough   | OpenMoHAA                                       |

- **Vanilla** is the last official Linux dedicated server. It's 32-bit and no longer maintained.
- **Reborn** is a community patch for Allied Assault that adds admin tools and fixes on top of the original game module. There's no Reborn for Spearhead or Breakthrough.
- **OpenMoHAA** is an open source engine that runs all three games from one native 64-bit binary, and players connect with the original game. Breakthrough never had a Linux dedicated server, so OpenMoHAA is the only way to run it.

New installs use `alliedassault-openmohaa`, saved to `lgsm/config-lgsm/mohaaserver/common.cfg` at install. Installs without a `variant` setting, including every install made before variants were added, use `alliedassault-reborn`.

### Changing Variant

Set `variant` in your instance config (`lgsm/config-lgsm/mohaaserver/mohaaserver.cfg`) and restart the server:

```
variant="spearhead-openmohaa"
```

LinuxGSM sets up OpenMoHAA or the vanilla files the next time it runs if they're missing. You can also pick the variant at install:

```
./mohaaserver auto-install --variant breakthrough-openmohaa
```

{% hint style="info" %}
`./mohaaserver details` shows the variant in use.
{% endhint %}

## Server Settings

| Setting      | Default                | Description                                                                                    |
| ------------ | ---------------------- | ---------------------------------------------------------------------------------------------- |
| `variant`    | `alliedassault-reborn` | Game and server build. New installs save `alliedassault-openmohaa`. See [Variants](#variants). |
| `defaultmap` | `dm/mohdm1`            | Map loaded on start.                                                                           |

The game config is:

```
serverfiles/main/mohaaserver.cfg
```

It holds the server name (`sv_hostname`), max players (`sv_maxclients`), the RCON password (`rconPassword`) and the server password (`g_password`). Every variant reads it, Spearhead and Breakthrough included. Restart the server after editing it.

For a Spearhead or Breakthrough server, set `defaultmap` to a map from that game.

## Ports

| Description | Port    | Protocol |
| ----------- | ------- | -------- |
| Game        | `12203` | UDP      |
| Query       | `12300` | UDP      |

Change them with `port` and `queryport` in your instance config. They become `+set net_port` and `+set net_gamespy_port`.

## Master Server

The original engines list servers on the GameSpy master, which has closed. The vanilla and Reborn variants use `master.gametir.com` instead, the master from the current Reborn release, so servers show in the in-game server browser. LinuxGSM changes the master in older engines on start, including those using `master.x-null.net`, which shuts down on 1 March 2027. Only the master address changes.

OpenMoHAA lists servers on the 333networks masters by default. See the [OpenMoHAA documentation](https://github.com/openmoh/openmohaa) to change them.

## Files

| Path                    | Contents                                                                        |
| ----------------------- | ------------------------------------------------------------------------------- |
| `serverfiles/main`      | Allied Assault game data and the game config                                    |
| `serverfiles/mainta`    | Spearhead game data                                                             |
| `serverfiles/maintt`    | Breakthrough game data                                                          |
| `serverfiles/vanilla`   | Original Allied Assault engine and game module, used by `alliedassault-vanilla` |
| `serverfiles/openmohaa` | OpenMoHAA, used by the OpenMoHAA variants                                       |
| `serverfiles/Logs`      | Game logs                                                                       |

## Server Resources

- [OpenMoHAA](https://github.com/openmoh/openmohaa)
- [MoH Reborn](https://www.mohreborn.com/)
- [333networks](https://333networks.com/)
