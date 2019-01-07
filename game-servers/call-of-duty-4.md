# Call of Duty 4

## CoD4x

`cod4server` uses CoD4x project for its server, rather than the original, as it fixes various bugs and adds a few features over the vanilla server.

[https://cod4x.me](https://cod4x.me)

## Getting Hold of Server Files

Many tutorials state that the game disk is required to install a CoD4 server. This is because the server is built in to the client. This made it difficult to distribute and create a CoD4 server.

After investigating this issue is was found that it is possible to run a server with most of the client files removed. This greatly reduces the file size and prevents the client from being used. Because of this LinuxGSM provides a download to only the files required to run the server. Preventing the use of the client and the opportunity to use the server to pirate the game.

## Updating CoD4x

CoD4x has its own update functionality. It will automatically check for updates and does not require LinuxGSM to check for updates.

## running mods 

To run a mod the servers fs_game variable must be set correctly. Mods reside in the mods folder inside fs_homepath.
Example directory tree:
mods/                                  
     ├── pml220                         
     │   ├── mod.ff                         
     │   ├── pml220.iwd                     
     │   ├── z_c_r.iwd

To start the server with a mod set the fs_game variable accordingly. 

`fn_parms(){
parms="+set sv_punkbuster 0 +set fs_basepath ${serverfiles} +set dedicated 1 +set net_ip ${ip} +set net_port ${port} +set sv_maxclients ${maxplayers} +exec ${servercfg} +map ${defaultmap} +set fs_game "mods/pml220""
}`

## Custom Maps

Modded CoD4 servers have the ability to run with user created maps.
To run a server with a custom map, it has to first be placed in the usermaps folder. In case that folder does not yet exist in your server directory just create it. Just like mods, connecting clients will have to download these maps first before playing them. As the CoD4 servers download speed is quite low, setting up a fast download server is recommended.

    ├── usermaps
    │   ├── mp_nuketown
    │   │   ├── mp_nuketown.ff
    │   │   ├── mp_nuketown.iwd
    │   │   ├── mp_nuketown_load.ff

Typically, maps are prefixed by mp_ following the maps name.

## Running custom maps on unmodded servers

Running custom maps on unmodded servers is not supported, but there is a neat workaround to still load custom maps. First create a mods folder and some empty folder inside it.

    ├── mods
    │   ├── myemptymod

Now set fs_game to mods/myemptymod and you will be able to run custom maps.

## Fast Download 
While players are able to download mods and custom maps of a server without any special configuration, this is only possible with a very limited download speed. Much more effective is the configuration of a fast download http server.
The following settings in your server configuration are necessary:
```
set sv_allowDownload "1" // allow clients to download gamefiles
set sv_wwwDownload "1" // enable download redirection
set sv_wwwBaseURL "http://domain.tld/cod4fastdl/" // defines url to download from
set sv_wwwDlDisconnected "0" // disconnect clients while downloading
```
here `sv_wwwBaseURL` has to point to a URL served by your http server.

An exaple directory tree for a served folder may look as blow:

    cod4fastdl/
    ├── mods
    │   ├── pml220
    │   │   ├── mod.ff
    │   │   ├── pml220.iwd
    │   │   ├── z_c_r.iwd
    ├── usermaps
    │   ├── mp_nuketown
    │   │   ├── mp_nuketown.ff
    │   │   ├── mp_nuketown.iwd
    │   │   ├── mp_nuketown_load.ff

## requirement for CoD4 X servers to get listed on masterserver
Gameservers need to prove now on registration at masterserver to have set a valid token in cvar sv_authtoken. If they can not prove to have this token they get rejected on masterserver. This requires a new version (17.6) of CoD4 X server you can download from the front-page. However the new version of CoD4 X server could still be less stable than the prior version as the core design is really new.

Do I need a token? Well if your server is still listed on [http://cod4master.cod4x.me/](http://cod4master.cod4x.me/) you don't need a token and don't need new serverversion yet unless you change your IP address.

 

Where do I get this token? You get it on: [https://cod4master.cod4x.me/](https://cod4master.cod4x.me/) and click the link "Get a Token". Here you need an unlimited and clean Steam account.

![image](https://i.imgur.com/dVXl8aL.png)

1.  What can I do with that token? Well you can either put into your server's commandline?
   * `+set sv_authtoken "mytokenhere"` or you edit your server.cfg file and add `set sv_authtoken "mytokenhere"`
 
2.  Can I use this token on multiple servers?
   * Yes this token is supposed to be used on all gameservers you own. Creating a new token will disable your old onw.

source from offcial cod4x forums more details click [here](https://cod4x.me/index.php?/forums/topic/2814-new-requirement-for-cod4-x-servers-to-get-listed-on-masterserver/) 





