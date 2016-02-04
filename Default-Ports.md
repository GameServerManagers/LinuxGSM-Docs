Changing default ports
------------
Default ports are most often set by start parameters. To alter them, which you probably want to do if you plan to run multiple servers, you will need to edit the main script file using vi or nano.

````nano gameserver````

For most games, you're gonna change these : 

    # Start Variables
    port="27015"
    sourcetvport="27020"
    clientport="27005"
    ip="0.0.0.0"

If you're running several servers, make sure you're using different ports on all of your servers.


### Protip for running many servers

If you plan on running more than 5 servers, you're probably want to make a table of your servers and ports in use.

### Ideas to set ports for multiple source servers

You can use any port you like in the 27000 range. Other values may work too.

**Method 1**

A good idea to be close the the steam standard but keep it simple, and be able to make 25 servers per hundred range, is to start with the first server that way : 

    port="27025"
    sourcetvport="27050"
    clientport="27000"

Then increment those port  by 1 for every new server. 25 servers are using 75 ports. After making 25 servers, if you need more, or if you want to separate servers, a good idea is to ad +100 to this 27000 range. Start this new server range this way : 

    port="27125"
    sourcetvport="27150"
    clientport="27100"


**Method 2**

You can use ports next to each other, like that : 

    port="27001"
    sourcetvport="27002"
    clientport="27000"

Some people find it more convenient. You'll be able to make more servers per hundred of ports that way (around 33 instead of 25), but, this is a non-standard way. 

**Method 3** 

You can get new IPs for your dedicated server, and assign some servers to different IPs.