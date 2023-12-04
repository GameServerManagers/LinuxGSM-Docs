# Garrys Mod

## Game Resources

[Garry's Mod Wiki](https://wiki.facepunch.com/gmod/)

## Server Tips

Autorefresh can lag the server when certain Lua files are edited. This happens when the refreshing cascades. This can be unwanted behaviour when editing the scripts of a large project on a live server.

To disable autorefresh, add `-disableluarefresh` to parms.

```
 -disableluarefresh
```

Loading screens are added by defining a website with `sv_loadingurl`, which is in gmodserver.cfg by default.  This file overrides other files.&#x20;

Links should not have `http://` or an ending`/` .&#x20;

Example:

```
sv_loadingurl "www.website.com/loading/screen"
```

Gamemode is changed by editing start parameters in the LinuxGSM config file.

```
Default gamemodes:

TTT     gamemode="terrortown"
Sandbox gamemode="sandbox"
```

Other gamemodes like Zombie Survival can be found on the [steam workshop](../../steamcmd/workshop.md).

### Workshop

{% content-ref url="../../steamcmd/workshop.md" %}
[workshop.md](../../steamcmd/workshop.md)
{% endcontent-ref %}

{% hint style="warning" %}
Garry's Mod does not require an API/Auth Key anymore.
{% endhint %}

For Garry's Mod, add the collection ID in [LinuxGSM config](../../configuration/linuxgsm-config.md) using `wscollectionid` setting. This will download the collection when the server starts.

```
wscollectionid="157384458"
```

###

## Guides

[Mounting Game Content To Garry's Mod Server](mounting-game-content.md)

[Install Sourcemod on Gmod Server](../../guides/sourcemod-csgo-server.md)
