# ATLAS

## Config Files default with LGSM

```text
serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
```

## REQUIRED Redis Server

```text
sudo apt install redis-server && redis-server
```

The default should work fine but custom password is recommended.

## Map

You can edit the map with the ServerGridEditor that can be found here [https://github.com/GrapeshotGames/ServerGridEditor](https://github.com/GrapeshotGames/ServerGridEditor)

More info on multiple Grids at the end of the page.

### Official Map Name:

* Ocean

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

All workshop mods can be found here [https://steamcommunity.com/app/834910/workshop/](https://steamcommunity.com/app/834910/workshop/).

## Grid Setup

Servers must be flagged as a homeserver via the ServerGrid tool to allow spawning in them, and use one of the freeport islands that has spawnpoints (otherwise players will spawn at the origin, though we'll be improving that to automatically spawn along the cost soon if no spawnpoints are found) Alternatively, you can launch a server with ```-ForceAllHomeServer``` to make all server/grid act as a homeserver and thus allow spawning on it.

## Exporting JSON config

Use your preferred tool to export(More details later).

### Starting an Atlas Server

Once you have your configuration exported you will end up with files like the following:

* ServerGrid.json
* ServerGrid.ServerOnly.json
* ServerGrid/*.jpg (Map images for display)

These will need to go into the ShooterGame/ folder. By default it looks for ```"ServerGrid"``` if you wish to use an alternative one you may run with the optional cmd line ```-GridConfig="MyServerConfig.json"```

Once those files are in place, you have to load up the ocean map with its coordinates on the grid.

Example: ```ShooterGameServer.exe Ocean?ServerX=1?ServerY=0?AltSaveDirectoryName=B1?MaxPlayers=100?ReservedPlayerSlots=30?QueryPort=57561?Port=5761?SeamlessIP=1.2.3.4 -log -server```

The important bits being which grid location to use ```?ServerX=1?ServerY=0``` and your own external IP ```?SeamlessIP=1.2.3.4``` This is your public facing IP, not an internal network one.

### ServerGrid.ServerOnly.json Values

```BaseServerArgs``` and ```MachineIdTag``` Don't actually do anything by default. We use them for our internal tools.
gridSize is the size in unreal units of each grid. We do not recommend going over ```1400000``` due to floating point precision issues.
```WorldAtlasId``` Set a unique id to make your servers line up
More to come soon!

### ServerGrid.json Values

DatabaseConnections This is your connection to Redis! Yes, you can keep them all the same, and they will share a connection. We will likely cut these down in the future.
Some Atlas Server ini values

## Game.ini

```[/Script/ShooterGame.ShooterGameMode]```

* bDontUseClaimFlags -- set this to disable claimflags entirely, on any grid
* NoClaimFlagDecayPeriodMultiplier -- set this value to scale-up the auto decay of any structures that are not witin a claimflag
* PlayerDefaultNoDiscoveriesMaxLevelUps -- how many level ups to allow players to achieve before discovery zone points are required (all remaining levelups up to the xp ramp limit are subdivided by the discoverzone points)
* bClampHomeServerXP -- limit levelling to a certain amount on a homeserver (requires that the server is also a homeserver)
* ClampHomeServerXPLevel -- what level to limit XP to on this homeserver.

## Current Gotchas

You must explicitly File->Save to save the project. Exporting does not save the project as is. This is likely to change in the future

**Additional Notes:** Servers which are running on local networks sometimes have trouble traveling to other grids. A fix I have found for this is adding '?MultiHome=0.0.0.0' to your command-line parameters.
**More info will be added soon**
