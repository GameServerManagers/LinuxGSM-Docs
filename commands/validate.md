# validate

{% hint style="info" %}
This is a command for game servers using [SteamCMD](../steamcmd/) only.
{% endhint %}

The `validate` command will check the server files to make sure they match the SteamCMD repository. This command is useful if game server files are deleted, corrupted or SteamCMD is failing to update.

Validation will overwrite any files that have been changed. This may cause issues with customised servers. For example, if you customise `mapcycle.txt`, this file will be overwritten to the server default. Any files that are not part of the default installation will not be affected. It is recommended you use this command only on initial installation and if there are server issues.

## Commands

Standard: `./gameserver validate`

Short: `./gameserver v`

