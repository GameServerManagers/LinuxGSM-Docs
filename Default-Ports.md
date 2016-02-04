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

Also, you can use any port close to those. A good idea to be able to make 25 servers per hundred range, is to start with the first server that way : 

    port="27025"
    sourcetvport="27050"
    clientport="27000"

Then increment them  by 1 at any new server. After making 25 servers, if you need more, or if you want to separate servers, a good idea is to ad +100. Start this new server range this way : 

    port="27125"
    sourcetvport="27150"
    clientport="27100"

Note : You can also get new IP ranges and assign some servers to different IPs.