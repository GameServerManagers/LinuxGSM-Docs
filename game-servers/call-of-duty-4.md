# Call of Duty 4

## Call of Duty 4 Server Files

Many tutorials state that the game disk is required to install a CoD4 server. This is because the server is built into the client. This made it difficult to distribute and create a CoD4 server.

After investigating this issue, it was found that it is possible to run a server with most of the client files removed. This greatly reduces the file size and prevents the client from being used. Because of this LinuxGSM provides a download to only the files required to run the server. Preventing the use of the client, removing the opportunity to use the server to pirate the game.

## CoD4x

`cod4server` uses CoD4x project for its server, rather than the original, as it fixes various bugs and adds a few features over the vanilla server.

[https://cod4x.ovh](https://cod4x.ovh)

### Updating CoD4x

CoD4x has its own update functionality. It will automatically check for updates and does not require LinuxGSM to check for updates.

### CoD4x Master Server

CoD4x game servers (since version 17.6) require a server token to be listed on the CoD4x master server.

To generate a token visit [here](https://cod4master.cod4x.me/index.php?token\_generator=true).

Once a token is generated add it to the `sv_authtoken` cvar in `server.cfg` or command-line parameters.

#### server.cfg

```
set sv_authtoken "mytokenhere"`
```

#### command-line parameters

```
+set sv_authtoken "mytokenhere"
```

The server then needs to be restarted to allow the game server to be listed.

[CoD4x master server list](http://cod4master.cod4x.me/)

[source](https://cod4x.me/index.php?/forums/topic/2814-new-requirement-for-cod4-x-servers-to-get-listed-on-masterserver/)

## Mod Support

Mods for Call of Duty 4 have to be manually added to the game server.

### Adding Mods

To run a mod the servers `fs_game` variable must be set correctly. Mods reside in the `mods` folder inside `fs_homepath`. Example directory tree:

```
mods/                                  
     ├── pml220                         
     │   ├── mod.ff                         
     │   ├── pml220.iwd                     
     │   ├── z_c_r.iwd
```

To start the server with a mod set the `fs_game` variable accordingly.

```
parms="+set sv_punkbuster 0 +set fs_basepath ${serverfiles} +set dedicated 1 +set net_ip ${ip} +set net_port ${port} +set sv_maxclients ${maxplayers} +exec ${servercfg} +map ${defaultmap} +set fs_game "mods/pml220""
```

## Custom Maps

Modded CoD4 servers have the ability to run with user-created maps. To run a server with a custom map, it has to first be placed in the `usermaps` directory (if missing simply create it yourself).

```
    ├── usermaps
    │   ├── mp_nuketown
    │   │   ├── mp_nuketown.ff
    │   │   ├── mp_nuketown.iwd
    │   │   ├── mp_nuketown_load.ff
```

Typically, maps are prefixed by mp\_ following the maps name.

## Running custom maps on unmodded servers

Running custom maps on unmodded servers is not supported, but there is a neat workaround to still load custom maps. First, create a mods folder and some empty folder inside it.

```
    ├── mods
    │   ├── myemptymod
```

Now set `fs_game` to `mods/myemptymod` and you will be able to run custom maps.

## Fast Download

[Fast download](../commands/fastdl.md) is possible with CoD4 to allow custom maps and mods to be hosted on a webserver.

```
set sv_allowDownload "1" // allow clients to download gamefiles
set sv_wwwDownload "1" // enable download redirection
set sv_wwwBaseURL "http://domain.tld/cod4fastdl/" // defines url to download from
set sv_wwwDlDisconnected "0" // disconnect clients while downloading
```

here `sv_wwwBaseURL` has to point to a URL served by your web server.

An example directory tree for a served folder may look as below:

```
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
```
