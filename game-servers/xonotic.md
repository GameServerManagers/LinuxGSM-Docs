# Xonotic

## Server Resources

[FAQ](https://xonotic.org/faq/)

## Ports

- Game Port Default: 26000 UDP

## Default Config Location

### Client Specific

As written in the FAQ, the default configuration files are located in:

| System | Location |
|--|--|
| Linux | $HOME/.xonotic/data/ |
| Windows | %USERPROFILE%\Saved Games\xonotic\ |
| MacOS | $HOME/Library/Application Support/xonotic/ |

### Server Hosting Locations

You can start Xonotic with the start parameter `-userdir`. With this parameter, Xonotic expects a subfolder `data` with the `server.cfg` in that directory. For example, if you choose `./xonotic-linux64-dedicated -userdir /home/xonotic/server1`, your `server.cfg` location should be `/home/xonotic/server1/data/server.cfg`.

## Game Modes

A list is currently located on [Xonotic Gitlab](https://gitlab.com/xonotic/xonotic/-/wikis/home#game-modes-or-game-types), with the following server parameters:

| Gametype | Server Value | Description |
|--|--|--|
| Deathmatch | dm | Classic Free-for-All mode where the player with the most frags wins |
| Team Deathmatch | tdm | Team-based mode where the team with the most frags wins |
| Capture the Flag | ctf | Team-based mode where the enemy flag has to be captured and brought back to your own base |
| Clan Arena | ca | Team- and round-based mode where the surviving team gets a point. Item pickups are absent |
| Freeze Tag | ft | Like Team Deathmatch, but killed players are frozen and can be revived by teammates. Ammo pickups are absent |
| Key Hunt | kh | Multi-team, round-based mode where one player from each team gets a key, and the team goal is to collect all keys |
| Assault | as | Team- and round-based mode where one team attacks and the other defends. Attackers try to destroy objectives as quickly as possible |
| Domination | dom | Multi-team-based mode where teams capture and control points on the map |
| Last Man Standing | lms | Free-for-All mode where players only respawn a limited number of times |
| Keepaway | ka | Free-for-All mode where you take a ball and, while equipped with it, frag opponents |
| Invasion | inv | Round-based PvE mode where players fight against monsters |
| Onslaught | ons | Team- and round-based mode where teams try to destroy the enemy generator |
| Race | rc | Free-for-All mode where players try to complete a track as quickly as possible |
| Complete the Stage | cts | Similar to the Race mode but with additional checkpoints to pass |
| Nexball | nb | Team- and round-based mode where teams try to shoot a ball into the enemy's goal |

## Custom Maps

### Server Side
Xonotic supports custom maps in the `pk3` file format. Maps should be placed in the `data` folder, like the `server.cfg`, on your dedicated server.

### Making It Usable for Clients
Xonotic doesn't provide a file downloader within the game server. You need to host your custom maps on HTTP webspace and set the correct values in `server.cfg`.

#### Example
- Userdir: `-userdir /home/xonotic/server1`: add `foo.pk3` to `/home/xonotic/server1/data/`
- `server.cfg`: Add `sv_curl_defaulturl="http://xonotic.foo.bar"`
- Put `foo.pk3` in the HTTP root folder to make it accessible via `http://xonotic.foo.bar/foo.pk3`

Check the [Xonotic Wiki](https://gitlab.com/xonotic/xonotic/-/wikis/Automatic-map-downloads) for more information about custom map hosting.

## Start Parameters

Every server cvar can be overridden by a start argument, but it's recommended to set up as much as possible in `server.cfg`.
