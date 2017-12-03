# Config Files
```
serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
```

# Adding Mods

1. Add `-automanagedmods` to the [[start parameters]]

2. Edit `GameUserSettings.ini`

Add the following line under `[ServerSettings]`
```
ActiveMods=[workshopID],[workshopID],[workshopID],[workshopID]
```
Replace `[workshopID]` with required workshop ID's.