# Config Files
```
serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
```

# Adding Mods

Add `-automanagedmods` to the [[start parameters]].

Next edit `GameUserSettings.ini`, adding the following line under `[ServerSettings]`.
```
ActiveMods=[workshopID],[workshopID],[workshopID],[workshopID]
```
Next edit `Game.ini` and add the following section.
```
[ModInstaller]
ModIDS=764326117
ModIDS=774762563
ModIDS=627340159
ModIDS=554678442
```
Replace `[workshopID]` with required workshop ID's.

All workshop mods can be found here http://steamcommunity.com/app/346110/workshop/.