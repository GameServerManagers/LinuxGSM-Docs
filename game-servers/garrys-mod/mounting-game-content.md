# Mounting Game Content

Some Garry's Mod addons like TTT use content from other games. This guide is for installing another game with LinuxGSM, copying that game's files, and mounting the game to Garry's Mod. This guide is for CS:S but should work for any other game.

First install a Counter-Strike: Source server, if you already have a server installed this step can be skipped. If the server will be deleted after copying files, the GSLT step is skippable.&#x20;

[Install CS:S Server with LinuxGSM](https://linuxgsm.com/servers/gmodserver/)

## Mounting one server

**Change the usernames to match yours.**&#x20;

Copy the cstrike folder to the Gmod folder.

```
cp -R /home/cssuser/serverfiles/cstrike/ /home/gmoduser/serverfiles/cstrike/
```

Recursively claim ownership of files for the gmod user.

```
chown -R gmoduser /home/gmoduser/
```

Open mount.cfg file.

```
nano /home/gmoduser/serverfiles/garrysmod/cfg/mount.cfg
```

Add game to mount.cfg

```
"mountcfg"
{
         "cstrike"      "/home/gmoduser/serverfiles/cstrike"
}
```

Restart the server. Check if the mount was successful by changing level to a mounted map with console or rcon.

```
changelevel cs_italy
```

If the CS:S user and install is no longer needed, it can be removed with userdel. **This command will remove the user and it's /home/ directory.**

```
userdel -r cssuser
```

##
