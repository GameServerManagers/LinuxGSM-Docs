# Counter-Strike 2

{% hint style="info" %}
This page is still a work in progress. If you have updated info please edit this document or let us know.
{% endhint %}

## **Server Resources**

### Official Server Resources

-   [CS 2 Dedicated server Wiki](https://developer.valvesoftware.com/wiki/Counter-Strike_2/Dedicated_Servers)
-   [CS 2 Game Modes](https://developer.valvesoftware.com/wiki/CS:GO_Game_Modes)

## **Game Modes**

CS2 features various game modes, which can be played on your server. To make setting up your server a bit easier, the following table sums up the configuration required in your server's [LinuxGSM config](../configuration/linuxgsm-config.md) for the various game modes. If you want more detailed and up-to-date information, take a look at Valve's wiki: [CS2 Game Modes](https://developer.valvesoftware.com/wiki/CS:GO_Game_Modes).&#x20;

| \[Game Modes]                     | gametype | gamemode | gamemodeflags | skirmishid | mapgroup (you can mix these across all Game Modes except Danger Zone, but use only one)                                                         |
| --------------------------------- | -------- | -------- | ------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
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

## Workshop

it is possible to add a single or collection of workshop maps to a Counter-Strike 2 server.

### Workshop ID

First, gather the map or collection ID. To do this find the workshop map or collection you want to use on the [CS2 steam workshop](https://steamcommunity.com/app/730/workshop/) and look at the URL; it will contain the required ID number. In the example below the ID is `3075706807`.

```text
https://steamcommunity.com/sharedfiles/filedetails/?id=3075706807
```

### Create a Collection

### Auth Key

If you are using a collection you will need to get an auth key from [here](https://steamcommunity.com/dev/apikey).
