You may want to add some start parameters to your server.

Here is a proper way to do it.


## Adding extra start parameters

The point is not to mess up with fn_parms all the time, so we're gonna add a new variable into the script that will contain your extra start parameters, then add the content of that variable into the fn_parms once for all, so you never touch it again. In other words, first time you add start parameters, you tweak the script by adding a new variable, but next times, you only need to change the value (content) of it.

Example : 

1. Edit your main script

`nano gameserver`

2. Find `# Start Variables` and add a new variable at the end of that section : 

`commands=""`

3. Inside of it, put any start option you like, for example

`commands="+r_hunkalloclightmaps 0 +tv_enable 0 -tickrate 33"`

4. Now, right under that, find `fn_parms(){` and add, at the end of it : 

`${commands}`

So you get something like this : 

`fn_parms(){
parms="-game gamename -strictportbind -ip ${ip} -port ${port} +host_workshop_collection ${workshopcollectionid} -authkey ${workshopauth} +clientport ${clientport} +tv_port ${sourcetvport} +gamemode ${gamemode} +map ${defaultmap} +sv_setsteamaccount ${gslt} +servercfgfile ${servercfg} -maxplayers ${maxplayers} ${commands}"
}`

5. Exit and save (with nano : ctrl + x, y, enter)

Enjoy your new parameters.
