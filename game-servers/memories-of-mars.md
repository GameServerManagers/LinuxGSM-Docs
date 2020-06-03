#Memories Of Mars

![](../.gitbook/assets/memories_of_mars.png)

# Resources
[Memories of Mars Wiki](https://memoriesofmars.gamepedia.com/Memories_of_Mars_Wiki)

[Memories of Mars Dedicated Server Wiki](https://memoriesofmars.gamepedia.com/Dedicated_Servers)


## Ports

* **Game Port*** Default:7777
* **Beacon Port*** Default:15000


## Required server config items
* ServerName >> This is the server name that you will find the server under in thein-game Server Browser or in the Steam Server Browser.
* ServerID >> By changing this, you can switch between different versions of the database (see section on database management).

## Command line arguments
* Port >> The port on which players connect. Make sure that this port is open in order for players to connect. Defaults to 7777.
* BeaconPort >> The port used for beacons for initial connection. Make sure that this port is open in order for players to connect over the internet. Defaults to 15000.
* MULTIHOME >> Overrides the IP address the server is running on. The server will use one of the available IP addresses but will not ascertain that this is a publicly reachable IP address. Used in Multi-IP environments.
* MaxPlayers >> Maximal number of players for the server. Default is 2.

# Database management
The files for the database will be stored in the following folder: Game/Saved/DB/{ServerID}/{SeasonID}.

You can create an easy backup of your files by copying everthing inside this folder and paste it elsewhere.

Once the game reaches a new season the database folder will create a new database inside a new season folder. The data from the previous season is still stored, but will not be used for the new season. The reason for that is, that we can not guarantee that the way the data is stored will not change between seasons. So you will start with a clean database in a new season, just like on the public servers.

If you are still willing to try to save your old data somehow you can try to manually copy the data over from the previous season. This might or might not work, depending on the changes made. So expect your game to cause some problems afterwards. If you can't get the game to run anymore after this just delete all the files you put in there and make sure you have a clean database.

NOTE: There will be no support by us for manually moving old databases to your newer server in case of database-breaking changes between seasons.

# Admin tools
Admins on a Dedicated Server are able to open an AdminTools window with F8. The key to show the window can be changed in the Input Settings (in case F8 doesn't work make sure it's bound there). From here you have the option to execute a selection of cheats to author your server.

# Known Issues
There will be two error messages on server start from Steam (Process Entry Point not found). Those can be clicked away without any issues and the server will run fine. Those error messages will be fixed in an upcoming version of the server.
