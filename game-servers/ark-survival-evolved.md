# Ark Survival Evolved

## Config Files

```text
serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
```

## Adding Mods

Add `-automanagedmods` to the [start parameters](../configuration/start-parameters.md).

Next edit `GameUserSettings.ini`, adding the following line under `[ServerSettings]`.

```text
ActiveMods=[workshopID],[workshopID],[workshopID],[workshopID]
```

Next edit `Game.ini` and add the following section. &lt;-- Doing this will auto download mods.

```text
[ModInstaller]
ModIDS=[workshopID]
ModIDS=[workshopID]
ModIDS=[workshopID]
ModIDS=[workshopID]
```

Replace `[workshopID]` with required workshop ID's.

All workshop mods can be found here [http://steamcommunity.com/app/346110/workshop/](http://steamcommunity.com/app/346110/workshop/).

## Collections

Collection Ids won't work directly. You need to have all the ids of the mods you want to use. One tool for getting the ids can be found here: [https://tools.rusty.info/tools/stcolids/](https://tools.rusty.info/tools/stcolids/)

