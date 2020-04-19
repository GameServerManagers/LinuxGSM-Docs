# Mounting Game Content

Some Garry's Mod addons use other game's content, this content must be mounted server-side otherwise players will be able to walk through props and other issues. The easiest way to add this content is to install a server with linuxgsm and copy the files over. This guide focuses on CS:S but should work for any game that can be mounted.

First install a Counter-Strike:Source server, if you already have a server installed this step can be skipped. If the server will be deleted after copying files, the GSLT step is skippable. 

[Install CS:S Server with LinuxGSM](https://linuxgsm.com/lgsm/cssserver/)

## Mounting one server

**Change the usernames in these commands to match yours.** 

Copy the cstrike folder to the Gmod folder.

```text
cp -R /home/cssuser/serverfiles/cstrike/ /home/gmoduser/serverfiles/cstrike/
```

Recursively claim ownership of moved files for the gmod install.

```text
chown -R gmoduser /home/gmoduser/
```

Open mount.cfg file.

```text
nano /home/gmoduser/serverfiles/garrysmod/cfg/mount.cfg
```

Add link to the files being mounted.

```text
"mountcfg"
{
         "cstrike"      "/home/gmoduser/serverfiles/cstrike"
}
```

Restart the server, and the content should now be mounted.

If the CS:S user and install is no longer needed, it can be removed with userdel. **This command will remove the user and it's /home/ directory.**

```
userdel -r cssuser
```

## 

