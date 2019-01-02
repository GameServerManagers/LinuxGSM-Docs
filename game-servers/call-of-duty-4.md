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
parms="+set sv_punkbuster 0 +set fs_basepath ${serverfiles} +set dedicated 1 +set net_ip ${ip} +set net_port ${port} +set sv_maxclients ${maxplayers} +exec ${servercfg} +map ${defaultmap} ++set fs_game "mods/pml220""
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
