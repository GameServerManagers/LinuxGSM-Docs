# Xonotic

## Server Resources

[FAQ](https://xonotic.org/faq/)

## Ports

- Game Port Default: 26000 UDP

## Default Config Location

### Client Specific

As written in the FAQ, the default Configuration files are located in:

| System | Location |
|--|--|
| Linux | $HOME/.xonotic/data/ |
| Windows | %USERPROFILE%\Saved Games\xonotic\ |
| MacOS | $HOME/Library/Application Support/xonotic/ |

### Serverhosting Locations

You can start Xonotic with the startparameter '-userdir'. With this parameter, Xonotic expects in that folder a subfolder `data` with the `server.cfg`. For example for choosing `./xonotic-linux64-dedicated -userdir /home/xonotic/server1` your server.cfg location should be `/home/xonotic/server1/data/server.cfg`

## Game Modes

A list is currently located in [Xonotic Gitlab](https://gitlab.com/xonotic/xonotic/-/wikis/home#game-modes-or-game-types). with the following server parameters

| Gametype | Servervalue | Description |
|--|--|--|
| Deathmatch | dm | Classic Free for All Gamemode where the player with the most frags wins |
| Team Deathmatch | tdm | Teambased Gamemode where the team with the most frags win |
| Capture the Flag | ctf | Teambased Gamemode where the enemy flag has to be captured and brought back to their own base |
| Clan Arena | ca | Team and Round-based Mode where the surviving team gets a point. Pickup Items are absent |
| Freeze Tag | ft | Like Teamdeathmatch, where killed players are frozen and can be revived by team members. Ammo Pickups are absent |
| Key Hunt | kh | Multiteam- and Roundbased Mode Mode where one player of each team gets a key and the team goal is to get all keys | 
| Assault | as | Team- and Round-based Mode where one Team is attacking and the other defending. Attackers try to destroy objects as fast as possible |
| Domination | dom | Multiteambased Gamemode where the teams capture and control points on the map |
| Last Man Standing | lms | Free for All Gamemode where you only respawn a certain amount of time |
| Keepaway | ka | Free for All Gamemode where you take a ball and with that equipped frag people |
| Invasion | inv | Roundbased PvE Gamemode where players fight against monsters |
| Onslaught | ons | Team and Roundbased Mode where the Team tries to destroy the enemy generator |
| Race | rc | Free for all Gamemode where players try to run over a track as fast as possible |
| Complete the Stage | cts | Like Race Gamemode with additional Checkpoints to pass |
| Nextball | nb | Team and Round-based Mode where teams try to shoot a ball to the enemy goal |

## Custom Maps

### Server side
Xonotic has Custom Maps support in fileformat `pk3`. Maps should be located in the data folder like `server.cfg` on your dedicated Server.

### Make it useable for Clients
Xonotic doesn't provide a Filedownloader inside the gameserver, have need to host your custommaps on HTTP Webspace and set the correct values in `server.cfg`.

#### Example
- Userdir: `-userdir /home/xonotic/server1`: add `foo.pk3`in  `/home/xonotic/server1/data/`
- `server.cfg`: Add `sv_curl_defaulturl="http://xonotic.foo.bar"`
- Put `foo.pk3` in the HTTP Root Folder to make it accessable via `http://xonotic.foo.bar/foo.pk3`

Look at [Xonotic Wiki](https://gitlab.com/xonotic/xonotic/-/wikis/Automatic-map-downloads) for more infos about Custom Map Hosting

## Start parameters

Every Server cvar can be overwritten in an starting argument, but it's recommended to setup as much as possible in `server.cfg`
