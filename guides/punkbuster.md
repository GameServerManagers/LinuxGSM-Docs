---
description: Enable PunkBuster anti-cheat on older Call of Duty, Battlefield, Quake and Wolfenstein servers
---

# PunkBuster

PunkBuster is an anti-cheat made by Even Balance. It was built into many shooters from about 2001 to 2015. It runs on the server as `pbsv.so` in a `pb` folder, and on each player's PC as a client. The server checks players, can take screenshots, and kicks or bans cheaters.

{% hint style="warning" %}
Even Balance no longer supports PunkBuster for any game LinuxGSM runs. There are no new cheat detections, no updates and no PunkBuster master servers for these titles. PunkBuster will still catch old, known cheats, and you can still use community ban lists. Treat it as a basic extra layer, not full protection.
{% endhint %}

LinuxGSM installs every server with PunkBuster turned off.

## Supported Servers

| Server                             | PunkBuster files                   |
| ---------------------------------- | ---------------------------------- |
| Battlefield 1942                   | Included                           |
| Battlefield: Vietnam               | Included                           |
| Call of Duty 2                     | Included                           |
| Quake 3: Arena                     | Included                           |
| Quake 4                            | Included                           |
| Soldier Of Fortune 2: Gold Edition | Included                           |
| Wolfenstein: Enemy Territory       | Included                           |
| Call of Duty: World at War         | Not included, download from PBBans |
| Call of Duty                       | Not available                      |
| Call of Duty: United Offensive     | Not available                      |
| Call of Duty 4                     | Not supported, LinuxGSM uses CoD4x |

"Included" means the `pb` folder that came with the original server files is already in `serverfiles/pb`.

Call of Duty 4 installs [CoD4x](https://cod4x.ovh), the maintained Linux server for CoD4. It works with 1.7 clients, but it doesn't support PunkBuster. LinuxGSM doesn't offer the official CoD4 server.

Return to Castle Wolfenstein, Jedi Knight II and Jedi Knight: Jedi Academy use open-source engines (iortcw and OpenJK) that don't include PunkBuster.

## Enable PunkBuster

1. Stop the server.
2. In `lgsm/config-lgsm/<x>server/<x>server.cfg`, copy the `startparameters` line from `_default.cfg` and change `+set sv_punkbuster 0` to `+set sv_punkbuster 1`. See [Start Parameters](../configuration/start-parameters.md).
3. Set the same value in the game config, where the game has one:
   - Quake 4: `seta sv_punkbuster "1"` in `serverfiles/q4base/server.cfg`.
   - Battlefield 1942 and Battlefield: Vietnam: `game.serverPunkBuster 1` in `serverfiles/mods/<mod>/settings/serversettings.con`. These two don't use the start parameter.
4. Start the server and check the console for PunkBuster loading.

{% hint style="info" %}
In the Quake 3 engine games, `sv_punkbuster` is read-only once the server is running. Set it in the start parameters, or use `pb_sv_enable` in the console.
{% endhint %}

## Add PunkBuster Files

Call of Duty: World at War doesn't come with PunkBuster files. Use this if you need them, or if a `pb` folder is missing or damaged:

1. Download the legacy server files for your game from [PBBans Legacy PunkBuster Files](https://community.pbbans.com/files/category/7-legacy-punkbuster-files/). Get both the Linux and Windows packages where both exist.
2. Stop the server.
3. Extract them into `serverfiles/pb`, so `pbsv.so` sits at `serverfiles/pb/pbsv.so`.
4. Make sure the files are owned by the LinuxGSM user, and that the user can write to `serverfiles/pb`. PunkBuster writes its logs, screenshots and settings there.
5. Enable PunkBuster as above.

{% hint style="warning" %}
LinuxGSM can't bundle these files. The PunkBuster licence doesn't allow redistribution, so download them yourself and accept the licence that comes with them.
{% endhint %}

## Configuration

PunkBuster reads its server settings from `serverfiles/pb/pbsv.cfg` when it starts. Create the file if it doesn't exist. For example, to turn on player screenshots:

```
pb_sv_ssflag 1
pb_sv_sspath "svss"
```

The full command list is in the archived PunkBuster server admin manuals on [PBBans](https://community.pbbans.com/files/category/7-legacy-punkbuster-files/).

## PBBans

[PBBans](https://www.pbbans.com) is a community ban network for PunkBuster games. It isn't run by Even Balance. Servers that stream to the PBBans Hub share bans, so a cheater banned on one server is blocked on all of them. It still accepts streams from the older games, including Call of Duty, Call of Duty 2, Call of Duty 4, Call of Duty: World at War, Battlefield 1942, Quake 4 and Enemy Territory.

To stream to PBBans:

1. Register on the [PBBans forums](https://community.pbbans.com).
2. Follow the PBBans Automated Hub Setup, which gives you the lines to add to `pbsv.cfg`.
3. Make sure the server's game port is reachable over UDP. PunkBuster streams over the same port the game uses.

## Server Resources

- [Even Balance](https://www.evenbalance.com)
- [PBBans](https://www.pbbans.com)
- [PBBans Legacy PunkBuster Files](https://community.pbbans.com/files/category/7-legacy-punkbuster-files/)
- [CoD4x](https://cod4x.ovh)
