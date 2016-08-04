## Default start parameters

LGSM comes with a bunch of start parameters that you can change within your "gameserver" script. So have a look at options proposed before anything else, it could save you some time.

## Extra start parameters

However, you may want to add some other start parameters to your server.

Here is a proper way to do it.

**Don't be lazy, read the whole guide ! Don't mess up with your main script !**


## Adding extra start parameters

The point is not to mess up with fn_parms all the time, so we're gonna add a new variables into the script that will contain your extra start parameters, then add the content of that variable into the fn_parms once for all, so you never touch it again. In other words, first time you add start parameters, you tweak the script by adding a new variable, but next times, you only need to change that variable's value.


### Example 

1. Edit your main script : `nano gameserver`

2.  Find `# Start Variables` and add a new `commands=""` variable at the end of that section

3. Inside of it, put any start option you like, for example : `commands="+r_hunkalloclightmaps 0 +tv_enable 0 -tickrate 33"`

4. Now, right under that, find `fn_parms(){ [code] }` and add `${commands}` at the end of it

So you get something like this : 

`fn_parms(){
parms="-game gamename -strictportbind -ip ${ip} -port ${port} +clientport ${clientport} +tv_port ${sourcetvport} +gamemode ${gamemode} +map ${defaultmap} +servercfgfile ${servercfg} -maxplayers ${maxplayers} ${commands}"
}`


Of course, save and exit (with nano : ctrl + x, y, enter), restart your server, and enjoy your new parameters.