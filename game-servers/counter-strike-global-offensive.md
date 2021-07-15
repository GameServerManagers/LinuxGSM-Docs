# Counter-Strike: Global Offensive

## **Server Resources**

**Official Server Resources**

* [CS:GO Dedicated server Wiki](https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Dedicated_Servers)
* [CS:GO Server Workshop setup Wiki](https://developer.valvesoftware.com/wiki/CSGO_Workshop_For_Server_Operators)
* [CS:GO Server Known Issues Wiki](https://developer.valvesoftware.com/wiki/CSGO_Game_Mode_Commands)

## **Server Tips**

Game Modes Reference List

```text
# [Game Modes]        gametype    gamemode    mapgroup (you can mix these across all Game Modes except Danger Zone, but use only one)
# Arms Race                    1            0                mg_armsrace
# Classic Casual          0            0                mg_casualsigma, mg_casualdelta
# Classic Competitive    0            1                mg_active, mg_reserves, mg_hostage, mg_de_dust2
# Custom                      3            0
# Deathmatch                1            2                mg_deathmatch
# Demolition                1            1                mg_demolition
# Wingman                      0            2
# Danger Zone                6            0                mg_dz_blacksite (map: dz_blacksite), mg_dz_sirocco (map: dz_sirocco)
```

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

