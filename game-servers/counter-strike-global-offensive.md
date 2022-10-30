# Counter-Strike: Global Offensive

## **Server Resources**

**Official Server Resources**

* [CS:GO Dedicated server Wiki](https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Dedicated_Servers)
* [CS:GO Server Workshop setup Wiki](https://developer.valvesoftware.com/wiki/CSGO_Workshop_For_Server_Operators)
* [CS:GO Server Known Issues Wiki](https://developer.valvesoftware.com/wiki/CSGO_Game_Mode_Commands)
* [CS:GO Game Modes](https://developer.valvesoftware.com/wiki/CS:GO_Game_Modes)

## **Game Modes**
CS:GO features various game modes, which can be played on your server. To make setting up your server a bit easier, the following table sums up the configuration required in your server's [LinuxGSM config](../configuration/linuxgsm-config.md) for the various game modes.
If you want more detailed and up-to-date information, take a look at Valve's wiki: [CS:GO Game Modes](https://developer.valvesoftware.com/wiki/CS:GO_Game_Modes). 
Up-to-date information about mapgroups can be found in the file `serverfiles/csgo/gamemodes.txt`.

| [Game Modes]                      | gametype | gamemode | gamemodeflags | skirmishid | mapgroup (you can mix these across all Game Modes except Danger Zone, but use only one)                                                         |
|-----------------------------------|----------|----------|---------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| Arms Race                         | 1        | 0        | 0             | 0          | mg_armsrace                                                                                                                                     |
| Boom! Headshot!                   | 1        | 2        | 0             | 6          | mg_skirmish_headshots                                                                                                                           |
| Classic Casual                    | 0        | 0        | 0             | 0          | mg_casualsigma, mg_casualdelta                                                                                                                  |
| Classic Competitive (Default)     | 0        | 1        | 0             | 0          | mg_active, mg_reserves, mg_hostage, mg_de_dust2, ...                                                                                            |
| Classic Competitive (Short Match) | 0        | 1        | 32            | 0          | mg_active, mg_reserves, mg_hostage, mg_de_dust2, ...                                                                                            |
| Danger Zone                       | 6        | 0        | 0             | 0          | mg_dz_blacksite (map: dz_blacksite), mg_dz_sirocco (map: dz_sirocco)                                                                            |
| Deathmatch (Default)              | 1        | 2        | 0             | 0          | mg_deathmatch                                                                                                                                   |
| Deathmatch (Free For All)         | 1        | 2        | 32            | 0          | mg_deathmatch                                                                                                                                   |
| Deathmatch (Team vs Team)         | 1        | 2        | 4             | 0          | mg_deathmatch                                                                                                                                   |
| Demolition                        | 1        | 1        | 0             | 0          | mg_demolition                                                                                                                                   |
| Flying Scoutsman                  | 0        | 0        | 0             | 3          | mg_skirmish_flyingscoutsman                                                                                                                     |
| Hunter-Gatherers                  | 1        | 2        | 0             | 7          | mg_skirmish_huntergatherers                                                                                                                     |
| Retakes                           | 0        | 0        | 0             | 12         | mg_skirmish_retakes                                                                                                                             |
| Stab Stab Zap                     | 0        | 0        | 0             | 1          | mg_skirmish_stabstabzap                                                                                                                         |
| Trigger Discipline                | 0        | 0        | 0             | 4          | mg_skirmish_triggerdiscipline                                                                                                                   |
| Wingman                           | 0        | 2        | 0             | 0          | mg_de_prime, mg_de_blagai, mg_de_vertigo, mg_de_inferno, mg_de_overpass, mg_de_cbble, mg_de_train, mg_de_shortnuke, mg_de_shortdust, mg_de_lake |

When adjusting the `mapgroup`, don't forget to also set `defaultmap` to a map contained in the same mapgroup.

If players are respawning in random locations on custom maps, set `mp_randomspawn` to 0.

If players are being banned for dying too much, such as on minigames maps, as a workaround set `mp_autokick` to 0. **Warning, this disables AFK and Teamkilling kicks as well.**

## **Server Guides**

[Install Sourcemod on CS:GO Server](../guides/sourcemod-csgo-server.md)

## **Setting for a 128 Tick Server**

Add to the following to the config `lgsm/config-lgsm/csgoserver/csgoserver.cfg` :

`tickrate="128"`

AS well it is needed to add a few options to the game config \(default in: `serverfiles/csgo/cfg/csgoserver.cfg` \)

```text
sv_mincmdrate 128
sv_minupdaterate 128
```

This will as well force the client to use the 128 tickrate

