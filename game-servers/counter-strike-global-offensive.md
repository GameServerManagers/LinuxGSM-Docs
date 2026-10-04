# Counter-Strike: Global Offensive

## **Server Resources**

**Official Server Resources**

* [CS:GO Dedicated server Wiki](https://developer.valvesoftware.com/wiki/Counter-Strike:\_Global\_Offensive\_Dedicated\_Servers)
* [CS:GO Server Workshop setup Wiki](https://developer.valvesoftware.com/wiki/CSGO\_Workshop\_For\_Server\_Operators)
* [CS:GO Server Known Issues Wiki](https://developer.valvesoftware.com/wiki/CSGO\_Game\_Mode\_Commands)
* [CS:GO Game Modes](https://developer.valvesoftware.com/wiki/CS:GO\_Game\_Modes)

## Client App ID

Since March 2026, CS:GO has been available on Steam as a standalone game (App ID `4465480`), separate from Counter-Strike 2 (App ID `730`). From v26.3.0, csgoserver has two App ID settings:

| Setting       | Default   | What it does                                                                                                         |
| ------------- | --------- | -------------------------------------------------------------------------------------------------------------------- |
| `appid`       | `740`     | The App ID SteamCMD downloads the dedicated server files from. Do not change.                                        |
| `clientappid` | `4465480` | The App ID the server advertises to players. Only clients of this App ID can connect, and your GSLT must be created for it. |

Choose `clientappid` based on which players you want to connect:

| Players using                      | `clientappid`       | Create the GSLT for |
| ---------------------------------- | ------------------- | ------------------- |
| Standalone CS:GO                   | `4465480` (default) | `4465480`           |
| Counter-Strike 2 `csgo_legacy` beta | `730`               | `730`               |

To change it, set it in `lgsm/config-lgsm/csgoserver/common.cfg`, as it applies to all instances sharing the same `serverfiles`:

```bash
clientappid="730"
```

A server advertises one App ID, so it serves one of these client types at a time. To serve both, run two separate installs: instances that share the same `serverfiles` would overwrite each other's `steam_appid.txt` and `steam.inf`.

LinuxGSM writes `clientappid` to `serverfiles/steam_appid.txt` and `serverfiles/csgo/steam.inf` before every start, because SteamCMD updates can revert them. Set `clientappid=""` if you want to manage these files yourself.

### NoLobbyReservation

Standalone CS:GO clients can only connect when the NoLobbyReservation SourceMod plugin is loaded. Install Metamod:Source, SourceMod and then NoLobbyReservation with the [mods commands](../commands/mods.md): run `./csgoserver mods-install` three times and select `metamodsource`, `sourcemod` and then `nolobbyreservation`. NoLobbyReservation can only be installed after SourceMod.

```
./csgoserver mods-install
```

NoLobbyReservation is only published as source code, so LinuxGSM compiles it with the SourceMod compiler during `mods-install` and `mods-update`.

### Upgrading from an earlier LinuxGSM version

{% hint style="warning" %}
After `update-lgsm`, existing CS:GO servers switch from App ID `730` to `4465480` the next time they start.

* **If your players use standalone CS:GO:** create a new GSLT for App ID `4465480`, set it as `gslt`, and install Metamod:Source, SourceMod and NoLobbyReservation (see [NoLobbyReservation](#nolobbyreservation)).
* **If your players use the CS2 `csgo_legacy` branch:** set `clientappid="730"` in `common.cfg` to keep the old behaviour. Your existing GSLT stays valid.
{% endhint %}

## **Game Modes**

CS:GO features various game modes, which can be played on your server. To make setting up your server a bit easier, the following table sums up the configuration required in your server's [LinuxGSM config](../configuration/linuxgsm-config.md) for the various game modes. If you want more detailed and up-to-date information, take a look at Valve's wiki: [CS:GO Game Modes](https://developer.valvesoftware.com/wiki/CS:GO\_Game\_Modes). Up-to-date information about mapgroups can be found in the file `serverfiles/csgo/gamemodes.txt`.

| \[Game Modes]                     | gametype | gamemode | gamemodeflags | skirmishid | mapgroup (you can mix these across all Game Modes except Danger Zone, but use only one)                                                                             |
| --------------------------------- | -------- | -------- | ------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Arms Race                         | 1        | 0        | 0             | 0          | mg\_armsrace                                                                                                                                                        |
| Boom! Headshot!                   | 1        | 2        | 0             | 6          | mg\_skirmish\_headshots                                                                                                                                             |
| Classic Casual                    | 0        | 0        | 0             | 0          | mg\_casualsigma, mg\_casualdelta                                                                                                                                    |
| Classic Competitive (Default)     | 0        | 1        | 0             | 0          | mg\_active, mg\_reserves, mg\_hostage, mg\_de\_dust2, ...                                                                                                           |
| Classic Competitive (Short Match) | 0        | 1        | 32            | 0          | mg\_active, mg\_reserves, mg\_hostage, mg\_de\_dust2, ...                                                                                                           |
| Danger Zone                       | 6        | 0        | 0             | 0          | mg\_dz\_blacksite (map: dz\_blacksite), mg\_dz\_sirocco (map: dz\_sirocco)                                                                                          |
| Deathmatch (Default)              | 1        | 2        | 0             | 0          | mg\_deathmatch                                                                                                                                                      |
| Deathmatch (Free For All)         | 1        | 2        | 32            | 0          | mg\_deathmatch                                                                                                                                                      |
| Deathmatch (Team vs Team)         | 1        | 2        | 4             | 0          | mg\_deathmatch                                                                                                                                                      |
| Demolition                        | 1        | 1        | 0             | 0          | mg\_demolition                                                                                                                                                      |
| Flying Scoutsman                  | 0        | 0        | 0             | 3          | mg\_skirmish\_flyingscoutsman                                                                                                                                       |
| Hunter-Gatherers                  | 1        | 2        | 0             | 7          | mg\_skirmish\_huntergatherers                                                                                                                                       |
| Retakes                           | 0        | 0        | 0             | 12         | mg\_skirmish\_retakes                                                                                                                                               |
| Stab Stab Zap                     | 0        | 0        | 0             | 1          | mg\_skirmish\_stabstabzap                                                                                                                                           |
| Trigger Discipline                | 0        | 0        | 0             | 4          | mg\_skirmish\_triggerdiscipline                                                                                                                                     |
| Wingman                           | 0        | 2        | 0             | 0          | mg\_de\_prime, mg\_de\_blagai, mg\_de\_vertigo, mg\_de\_inferno, mg\_de\_overpass, mg\_de\_cbble, mg\_de\_train, mg\_de\_shortnuke, mg\_de\_shortdust, mg\_de\_lake |

When adjusting the `mapgroup`, don't forget to also set `defaultmap` to a map contained in the same mapgroup.

If players are respawning in random locations on custom maps, set `mp_randomspawn` to 0.

If players are being banned for dying too much, such as on minigames maps, as a workaround set `mp_autokick` to 0. **Warning, this disables AFK and Teamkilling kicks as well.**

## **Server Guides**

[Install Sourcemod on CS:GO Server](../guides/sourcemod-csgo-server.md)

## **Setting for a 128 Tick Server**

Add to the following to the config `lgsm/config-lgsm/csgoserver/csgoserver.cfg` :

`tickrate="128"`

AS well it is needed to add a few options to the game config (default in: `serverfiles/csgo/cfg/csgoserver.cfg` )

```
sv_mincmdrate 128
sv_minupdaterate 128
```

This will as well force the client to use the 128 tickrate

## Workshop

For CSGO, edit these lines in your [LinuxGSM config](../configuration/linuxgsm-config.md)

```
wsapikey="YOUR_STEAM_API_KEY"
wscollectionid="YOUR_COLLECTION_ID"
wsstartmap="
```
