# Holdfast: Nations At War

## Requirements

- At least 2 GB of RAM. An idle server uses about 1 GB.

The dedicated server downloads anonymously with SteamCMD (App ID `1424230`, about 10 GB), so no Steam login is needed.

## Server Settings

Nearly all settings live in the game config, not in LinuxGSM config. Each instance has its own file:

```
serverfiles/serverconfig_hfserver.txt
```

The file name follows the instance name, so a second instance `hfserver-2` uses `serverconfig_hfserver-2.txt`. On install LinuxGSM copies it from the shipped `serverconfig_default.txt`, sets `server_name` to `LinuxGSM` and sets a random `server_admin_password`. Run `./hfserver details` to see the path and the values LinuxGSM reads from it.

The file uses `key value` lines, with `#` for comments. Stop the server before editing it, then start it again.

| Setting                 | Description                                          |
| ----------------------- | ---------------------------------------------------- |
| `server_name`           | Name shown in the server browser.                    |
| `server_password`       | Password players need to join. Leave empty for none. |
| `server_admin_password` | Password for in-game admin login.                    |
| `server_port`           | Game port.                                           |
| `steam_query_port`      | Steam query port.                                    |
| `maximum_players`       | Maximum number of players.                           |

### Map Rotation

Maps and game modes are set in `!map_rotation start` and `!map_rotation end` blocks in the same file. Sample rotations ship in:

```
serverfiles/example_map_rotations/
```

Copy the blocks you want into your game config. The [official hosting guide](https://wiki.holdfastgame.com/Server_Hosting) lists the maps, game modes and other settings each block takes.

## Ports

| Description | Port    | Protocol |
| ----------- | ------- | -------- |
| Game        | `20100` | UDP      |
| Steam query | `27000` | UDP      |

Change ports with `server_port` and `steam_query_port` in the game config. For a second instance, change both in that instance's `serverconfig_<instance>.txt` so they don't clash with the first.

LinuxGSM monitors the server with a Steam (A2S) query on `steam_query_port`.

## Files

| Path                                      | Contents                                       |
| ----------------------------------------- | ---------------------------------------------- |
| `serverfiles/serverconfig_<instance>.txt` | Game config for each instance.                 |
| `serverfiles/logs_chat/`                  | Chat log, `chatlog_<instance>.txt`.            |
| `serverfiles/logs_playerlogin/`           | Player logins, `playerlogin_<instance>.txt`.   |
| `serverfiles/logs_adminactions/`          | Admin commands, `adminactions_<instance>.txt`. |
| `serverfiles/logs_score/`                 | Scoreboard, `scorelog_<instance>.txt`.         |
| `serverfiles/logs_vac/`                   | VAC events, `vaclog_<instance>.txt`.           |
| `serverfiles/bannedplayers.txt`           | Banned players.                                |
| `serverfiles/muteplayerschat.txt`         | Players muted in chat.                         |
| `serverfiles/muteplayersvoip.txt`         | Players muted on voice.                        |
| `serverfiles/micspammers.txt`             | Mic spammers.                                  |

The main server output goes to the LinuxGSM game log in `log/server/`.

## Server Resources

- [Holdfast Server Hosting (official wiki)](https://wiki.holdfastgame.com/Server_Hosting)
