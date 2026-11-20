# Minecraft

## Requirements

- Java. LinuxGSM checks the installed Java against the Minecraft version you set: Java 25 for `latest` and Minecraft 26.1 or newer, Java 21 for Minecraft 1.20.5 to 1.21.x.
- At least 1 GB of RAM for the server (`javaram`). Modded servers usually need more.

LinuxGSM downloads the server from the official source for each [variant](#variants), not from Steam.

## Server Settings

Instance settings go in `lgsm/config-lgsm/mcserver/mcserver.cfg`.

### Release Settings

| Setting     | Default   | Description                                                                                              |
| ----------- | --------- | -------------------------------------------------------------------------------------------------------- |
| `variant`   | `vanilla` | Server build to install: `vanilla`, `fabric`, `forge`, `neoforge`, `paper`, `purpur`, `folia` or `leaf`. |
| `branch`    | `release` | `release` for stable versions, `snapshot` for development versions.                                      |
| `mcversion` | `latest`  | `latest`, or a specific Minecraft version such as `1.21.10`.                                             |
| `javaram`   | `1024`    | Maximum Java heap in MB, passed as `-Xmx`.                                                               |

The game settings live in `server.properties`. Restart the server after editing it.

```
serverfiles/server.properties
```

## Variants

One `mcserver` script installs and switches between these server builds:

| Variant    | Name     | Type                               | Downloaded from    |
| ---------- | -------- | ---------------------------------- | ------------------ |
| `vanilla`  | Vanilla  | Official Mojang server             | mojang.com         |
| `fabric`   | Fabric   | Mod loader                         | fabricmc.net       |
| `forge`    | Forge    | Mod loader                         | minecraftforge.net |
| `neoforge` | NeoForge | Mod loader                         | neoforged.net      |
| `paper`    | PaperMC  | Plugin server                      | papermc.io         |
| `purpur`   | Purpur   | Plugin server, fork of Paper       | purpurmc.org       |
| `folia`    | Folia    | Plugin server, multithreaded Paper | papermc.io         |
| `leaf`     | Leaf     | Plugin server, fork of Paper       | github.com         |

### Choosing a Variant on Install

`./mcserver install` asks which variant and Minecraft version to install. To skip the questions, pass them as options:

```
./mcserver install --variant fabric --version 1.21.10
```

`--variant` sets `variant` and `--version` sets `mcversion` in your config. If a config file already sets `variant`, LinuxGSM writes the new value there, otherwise it writes to `common.cfg`.

{% hint style="info" %}
Options need an up-to-date `mcserver` script. If LinuxGSM says so, run `./mcserver update-lgsm` first.
{% endhint %}

### Switching Variant

Change the variant on an existing server with `update`:

```
./mcserver update --variant paper
```

You can also set `variant` in your config and run `./mcserver update`. LinuxGSM records the installed variant in `serverfiles/variant.txt`. When it differs from `variant`, the next update installs the new variant.

{% hint style="warning" %}
Take a backup before changing variant: `./mcserver backup`.

- Mods and plugins aren't shared between variants. Fabric, Forge and NeoForge mods only load on their own loader, so replace them with builds for the new one.
- Paper, Purpur, Folia and Leaf keep the Nether and End in `world_nether` and `world_the_end`. Vanilla, Fabric, Forge and NeoForge don't load them from there.
- Folia only loads plugins that declare Folia support.
{% endhint %}

### Forge

- Forge is supported for Minecraft 1.17 and newer only.
- LinuxGSM installs the recommended Forge build for your Minecraft version, or the latest build when there's no recommended one.

### NeoForge

- NeoForge versions follow the Minecraft version: Minecraft `1.21.10` uses NeoForge `21.10.x`, and Minecraft `26.3` uses NeoForge `26.3.0.x`. LinuxGSM picks the newest NeoForge build for your `mcversion`.
- Beta builds are only used when `branch="snapshot"`.

### Forge and NeoForge Start Arguments

Forge and NeoForge install with their own installer and start with `@user_jvm_args.txt @unix_args.txt` instead of a server jar. LinuxGSM still adds `-Xmx` from `javaram`. Put any extra JVM options in `serverfiles/user_jvm_args.txt`.

## Updates

`./mcserver update` checks the source for your variant and installs the newest build for your `branch` and `mcversion`. Set `mcversion` to a specific version to stay on it.

A Minecraft release is either a _release_ (stable) or a _snapshot_ (still under development). Vanilla and Fabric use `branch` to choose between them. NeoForge only uses beta builds on `snapshot`.

{% hint style="warning" %}
Minecraft can't load a world saved by a newer version. Once a world has run on a version, you can't go back to an older `mcversion` with it. Take a backup before updating to a new Minecraft version.
{% endhint %}

## Files

| Path                            | Contents                                          |
| ------------------------------- | ------------------------------------------------- |
| `serverfiles/server.properties` | Game settings                                     |
| `serverfiles/variant.txt`       | Installed variant                                 |
| `serverfiles/build.txt`         | Installed build, for every variant except vanilla |
| `serverfiles/user_jvm_args.txt` | Extra JVM options (Forge and NeoForge)            |
| `serverfiles/mods`              | Mods (Fabric, Forge and NeoForge)                 |
| `serverfiles/plugins`           | Plugins (Paper, Purpur, Folia and Leaf)           |
| `serverfiles/logs`              | Game logs                                         |

## Server Resources

- [List of Minecraft Java releases](https://minecraft.wiki/w/Java_Edition_version_history)
- [List of Minecraft Java snapshots](https://minecraft.wiki/w/Java_Edition_version_history/Development_versions)
- [Fabric](https://fabricmc.net/)
- [Forge](https://files.minecraftforge.net/)
- [NeoForge](https://neoforged.net/)
- [PaperMC and Folia](https://papermc.io/)
- [Purpur](https://purpurmc.org/)
- [Leaf](https://github.com/Winds-Studio/Leaf)
