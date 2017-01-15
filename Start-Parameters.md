Servers commonly require start parameters, these are command-line options that are set with the servers executable when you start the server. Your current parameters can be found in `./gameserver details`. To alter them, you will need to edit the main script file `nano gameserver`.

# Pre-defined start parameters

LinuxGSM often comes with pre-defined parameters that you can edit. This is designed to make adjusting common settings a little easier. 

_Example of pre-defined parameters_

    ## Server Start Settings
    defaultmap="map_name"
    gamemode="game_mode"
    maxplayers="42"
    port="27015"
    sourcetvport="27020"
    clientport="27005"

# Additional Parameters

Additional command-line parameters can be added to the parms variable. Anything added will be appended to the server executable binary.

_Parms Variable_
   ` parms="-game tf"`

_Executable_
    `./srcds_run -game tf`

_Full Parms Example_
```
## Server Start Parameters | https://github.com/GameServerManagers/LinuxGSM/wiki/Start-Parameters
fn_parms(){
parms="-game nmrih -insecure -strictportbind -ip 91.121.72.41 -port 27015 +clientport 27017 +tv_port 27016 +map nmo_broadway +servercfgfile nmrih-server-1.cfg -maxplayers 8"
}
```
## Parameters reference
* 7 Days to Die http://7daystodie.gamepedia.com/Server
* Source Dedicated Servers: https://developer.valvesoftware.com/wiki/Command_Line_Options#Source_Dedicated_Server