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

New installs use `alliedassault-openmohaa`, saved to `lgsm/config-lgsm/mohaaserver/common.cfg` at install. Installs without a `variant` setting, including every install made before variants were added, use `alliedassault-reborn`.

Players connect with their normal copy of the game whichever build the server runs, but they need the game the server is running: Spearhead for a Spearhead server, Breakthrough for a Breakthrough server.

### Vanilla

The vanilla variants run the last official Linux dedicated servers: 1.11 for Allied Assault and 2.15 for Spearhead. They're the closest match to how the game shipped, but they're 32-bit, haven't been updated in over 20 years and have known exploits that were never patched.

`alliedassault-vanilla` runs from `serverfiles/vanilla`, because the 1.11 engine loads its game module from its own directory and the Reborn module sits at the root. Use it only if you need an unmodified server, for example to rule out Reborn when tracking down a problem.

### Reborn

MoH Reborn is a community patch that takes Allied Assault to version 1.12. It replaces the server's game module with one that adds admin tools and fixes for known exploits and crashes, and loads the original module underneath it, so gameplay is unchanged. It runs on a patched copy of the 32-bit 1.11 engine.

Reborn only exists for Allied Assault. `alliedassault-reborn` is the fallback for installs with no variant, so servers set up before variants keep running exactly as before.

{% hint style="info" %}
On start, Reborn may log `You are using different version of mohaa_lnxded`. It's a version check in the Reborn module and can be ignored: the server runs normally.
{% endhint %}

### OpenMoHAA

OpenMoHAA is an open source rewrite of the engine and game code. One native 64-bit binary runs Allied Assault, Spearhead and Breakthrough, picked with `com_target_game` (0, 1 or 2), which the variant sets for you. It reads the same game data from `main`, `mainta` and `maintt`, and the original game clients connect to it.

It's actively developed and fixes many of the original bugs and exploits, but it's still pre-1.0 (LinuxGSM installs v0.82.1), so expect the odd difference from the original game. Breakthrough never had a Linux dedicated server, so `breakthrough-openmohaa` is the only way to run it on Linux.

### Choosing a Variant

- **Allied Assault:** `alliedassault-openmohaa` for a 64-bit, maintained server. `alliedassault-reborn` if you want the Reborn admin tools or the original engine's behaviour.
- **Spearhead:** `spearhead-openmohaa`, unless you need the original 2.15 server, in which case use `spearhead-vanilla`.
- **Breakthrough:** `breakthrough-openmohaa`, the only option.

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

The in-game server browser gets its list of servers from a master server. Each server sends a heartbeat to it so players can find it.

- **GameSpy:** the original engines report to `master.gamespy.com`. GameSpy shut down its master servers in 2014, so these servers no longer appear in the browser.
- **xNULL:** the community group xNULL ran a replacement master, `master.x-null.net`, and released engines patched to use it, which earlier LinuxGSM installs used. xNULL is closing, and its master shuts down on 1 March 2027.
- **gametir:** the current MoH Reborn release moves its engines to `master.gametir.com`, run on 333networks infrastructure. The engines are the same as the xNULL ones apart from the master address.

The vanilla and Reborn variants use `master.gametir.com`. New installs get the current engines, and on start LinuxGSM changes the master address in the known GameSpy and xNULL engines, so older installs move over without reinstalling. Nothing else in the engine changes.

OpenMoHAA lists servers on the 333networks masters by default, and isn't affected by the xNULL shutdown. See the [OpenMoHAA documentation](https://github.com/openmoh/openmohaa) to change them.

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
