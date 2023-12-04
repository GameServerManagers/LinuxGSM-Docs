# Mounting Game Content

Some Garry's Mod addons like TTT use content from other games. To do this the content will need to be "mounted".

{% hint style="success" %}
All source engine games should be mountable.
{% endhint %}

## &#x20;Basic Guide

This guide is for installing another game server with LinuxGSM and use that content, copying that game's files, and mounting the game to Garry's Mod. This guide is for CS:S but should work for any other game.

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

##
