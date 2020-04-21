# Garrys Mod

## Game Resources

[Garry's Mod Wiki](https://wiki.facepunch.com/gmod/)

## Server Tips

Autorefresh can lag the server when certain Lua files are edited. This happens when the refreshing cascades. This can be unwanted behaviour when editing the scripts of a large project on a live server.

To disable autorefresh, add `-disableluarefresh` to parms.

```text
 -disableluarefresh
```

Loading screens are added by defining a website with `sv_loadingurl`, which is in gmodserver.cfg by default.  This file overrides other files. 

Links should not have `http://` or an ending`/` and should look like 

```text
sv_loadingurl "www.website.com/loading/screen"
```

Server gamemode is changed by editing start parameters in the file:

/home/user/linuxgsm/config-linuxgsm/gmodserver/gmodserver.cfg

On a new server, default settings are in default.cfg

```text
Default gamemodes- for use in command line

TTT     gamemode="terrortown"
Sandbox gamemode="sandbox"
```

Other gamemodes like Zombie Survival can be found in the [steam workshop](../../steamcmd/workshop.md).

## Guides

[Mounting Game Content To Garry's Mod Server](mounting-game-content.md)

[Install Sourcemod on Gmod Server](../guides/sourcemod-csgo-server.md)

