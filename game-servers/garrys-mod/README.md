# Garry's Mod

## Game Resources

[Garry's Mod Wiki](https://wiki.facepunch.com/gmod/)

## Auto Refresh

Autorefresh can lag the server when certain Lua files are edited. This happens when the refreshing cascades. This can be unwanted behavior when editing the scripts of a large project on a live server.

To disable autorefresh, add `-disableluarefresh` to parms.

```
 -disableluarefresh
```

## Loading Screen

Loading screens are added by defining a website with `sv_loadingurl`, which is in `gmodserver.cfg` by default.  This file overrides other files. &#x20;

{% hint style="warning" %}
Links should not have `http://` or an ending`/` .
{% endhint %}

```
sv_loadingurl "www.website.com/loading/screen"
```

## Gamemode

Gamemode is changed by editing start parameters in the LinuxGSM config file.

```
TTT     gamemode="terrortown"
Sandbox gamemode="sandbox"
```

Other game modes like Zombie Survival can be found on the [steam workshop](../../steamcmd/workshop.md).

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

## Mounting Game Content

Some Garry's Mod addons like TTT use content from other games. To do this the content will need to be "mounted".

{% hint style="success" %}
All source engine games should be mountable.
{% endhint %}

This guide is for installing another game server with LinuxGSM and using that content, copying that game's files, and mounting the game to Garry's Mod. This guide is for CS:S but should work for any other game.

{% hint style="info" %}
There are multiple ways to potentially mount content. The below example is just one example
{% endhint %}

First install a Counter-Strike: Source server, if you already have a server installed this step can be skipped. If the server will be deleted after copying files.

[Install CS:S Server with LinuxGSM](https://linuxgsm.com/servers/cssserver/)

Copy the `cstrike` the directory from the Counter-Strike: Source to the Gmod folder.

```
cp -R /home/cssserver/serverfiles/cstrike /home/gmodserver/serverfiles/cstrike
```

Ensure that the copied files are owned by the `gmodserver`  user.

```
chown -R gmodserver /home/gmodserver
```

Open mount.cfg file.

```
nano /home/gmodserver/serverfiles/garrysmod/cfg/mount.cfg
```

Add game to mount.cfg

```
"mountcfg"
{
         "cstrike"      "/home/gmoduser/serverfiles/cstrike"
}
```

Restart the server. Check if the mount was successful by changing the level to a mounted map with console or rcon.

```
changelevel cs_italy
```

