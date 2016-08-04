Servers commonly require start parameters that are command-line options which are set with the servers executable when you start the server. Your current parameters can be found in `./gameserver details`. To alter them, you will need to edit the main script file using `vi` or `nano`.

## Additional Parameters

Additional command-line parameters can be added to the parms variable. Anything added will be appended to the server executable binary.

_Parms Variable_
   ` parms="-game tf"`

_Executable_
    `./srcds_run -game tf`

_Full Parms Example_

    fn_parms(){
    parms="-game nmrih -insecure -strictportbind -ip 91.121.72.41 -port 27015 +clientport 27017 +tv_port 27016 +map nmo_broadway +servercfgfile nmrih-server-1.cfg -maxplayers 8"
    }

## Pre-defined start parameters

LGSM sometimes comes with a bunch of pre-defined parameters that you can edit.

_Example of pre-defined parameters_

    # Start Variables
    defaultmap="map_name"
    gamemode="game_mode"
    maxplayers="42"
    port="27015"
    sourcetvport="27020"
    clientport="27005"

## Adding start parameters

1. Edit the main script: `nano gameserver`

2. Find `# Start Variables`

3. Append any additional parameters to the parms variable

4. Save and exit (with nano : ctrl + x, y, enter), restart your server, and enjoy your new parameters.