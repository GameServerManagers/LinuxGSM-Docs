# Ark Survival Evolved

## Config Files

```text
serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
```

## Change Map

You can change the map by editing the [instance config](../configuration/linuxgsm-config.md) `lgsm/config-lgsm/arkserver/arkserver.cfg`.

Add the line `defaultmap="MAP_NAME_HERE"`. You can find a official map list right below.

### Official Map Names:

* TheIsland
* TheCenter
* Ragnarok
* ScorchedEarth\_P
* Aberration\_P
* Extinction
* Valguero\_P

## Change maximum players

You can change the number of maximum players by editing the [instance config](../configuration/linuxgsm-config.md) `lgsm/config-lgsm/arkserver/arkserver.cfg`.

Add the line `maxplayers=70`.

## Adding Mods

Add `-automanagedmods` to the [start parameters](../configuration/start-parameters.md).

Next edit `GameUserSettings.ini`, adding the following line under `[ServerSettings]`.

```text
ActiveMods=[workshopID],924619115,924619116,924619117
```

Next edit `Game.ini` and add the following section. &lt;-- Doing this will auto download mods.

```text
[ModInstaller]
ModIDS=[workshopID]
ModIDS=924619115
ModIDS=924619116
ModIDS=924619117
```

Replace `[workshopID]` with required workshop ID's.

All workshop mods can be found here [http://steamcommunity.com/app/346110/workshop/](http://steamcommunity.com/app/346110/workshop/).

## Collections

Collection Ids won't work directly. You need to have all the ids of the mods you want to use. One tool for getting the ids can be found here: [https://tools.rusty.info/tools/stcolids/](https://tools.rusty.info/tools/stcolids/)

## Clusters

First you need to setup [multiple ARK game server instances](../features/multiple-game-servers.md).

To change command-line parameters for your server edit  `lgsm/config-lgsm/arkserver/arkserver-2.cfg`_'_. Example:

```text
fn_parms(){
  parms="\"TheIsland?SessionName=MyServerName1?AltSaveDirectoryName=Save1?Port=7777?QueryPort=27015" -NoTransferFromFiltering -clusterid=cluster1\""
}
```

**Additional Notes:** Servers which are running on local networks sometimes have trouble travelling to other arks. A potential fix for this is adding `?MultiHome=0.0.0.0` to your command-line parameters.

