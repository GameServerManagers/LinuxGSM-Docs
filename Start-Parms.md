You may want to add some start parameters to your server.

Here is a proper way to do it.


## Adding extra start parameters

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
parms="-game gamename -strictportbind -ip ${ip} -port ${port} +host_workshop_collection ${workshopcollectionid} -authkey ${workshopauth} +clientport ${clientport} +tv_port ${sourcetvport} +gamemode ${gamemode} +map ${defaultmap} +sv_setsteamaccount ${gslt} +servercfgfile ${servercfg} -maxplayers ${maxplayers} ${command}"
}`

5. Exit and save (with nano : ctrl + x, y, enter)

6. Enjoy your new parameters.

Next time, when you need to change it, you will only need to edit your "commands" variable, which is way more simple and safe than messing with fn_parms directly all the time. 