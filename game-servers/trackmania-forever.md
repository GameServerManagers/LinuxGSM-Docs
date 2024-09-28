# Trackmania Nations Forever / Trackmania United Forever
![TMNF Logo](https://www.gamers.org/tmf/banner.jpg)

## Ports

- Game Port Default: 2350 UDP
- P2P Port for downloading Custom Maps / Files: 3450 TCP
- XMLRPC Port: 5000 TCP

## Online Hosting Requirements

Hosting an Internet accessable Online Server requieres a login to the master server. It can't be your game login and every server needs an unique account. 

For LAN Hosting a server login isn't required!

### Trackmania Nations Forever Server Account

- Start your gameclient and create an account there

### Trackmania United Forever Server Account

- Login with your gaming credentials at http://official.trackmania.com/tmf-playerpage/ (either use http or setup your browser to support older https protocols)
- On "Dedicated servers" you have to type your Serial Code of the Game to allow access of dedicated server accounts. If your bought Trackmania United Forever on Steam it's easy to get your product code
- Create there a new login for the dedicated Server

## Startparameters

Startparameters override Settings in the configuration of `dedicated_cfg`

| Startparameter | Function
|--|--|
| dedicated_cfg=xxx | Specifies the name of the dedicated configuration |
| game_settings=xxx | Specifies the name of game settings configuration |
| login=xxx | Username of Server Account |
| password=xxx | Password of Server Account |
| servername=xxx | Name of the Server |
| serverpassword=xxx | Connection Password for clients to connect if you want to make the server private |
| lan | Start server in LAN mode |
| forceip=xxx(:xx) | Forces the public ip address (and optionally port) to this value |
| bindip=xxx(:xx) | Binds server to ip address if multiple network interfaces are on the machine |
| join=xxx | Joins a server, to make a relay server. (xxx = the server ip adress with optional port, or the server login) |
| joinpassword=xxx | Password to use to join the remote server if the server is private |
| loadcache | Loads the "checksum.txt" instead of recomputing it, to speed up first launch time if P2P is enabled. *DO NOT USE* if you run several servers in the same directory |
| nologs | Disables the creation of "GameLog.txt" and "ConsoleLog.txt" in Logs/ directory |
| noautoquit | Keeps the server running "waiting for rpc commands", even if it is not live (with a map loaded and ready to receive players) |
| nodaemon | Doesn't detach the process |
| verbose_rpc_full | Display the whole contents of the xml-rpc requests the dedicated server receives. |
| verbose_rpc | Displays the xml-rpc requests the dedicated server receives, but only the name of the XmlRpc? command and some parameters |

Example: `TrackmaniaServer /dedicated_cfg=dedicated_cfg.txt /game_settings=MatchSettings/custom_game_settings.txt /nodaemon /lan`

Source of parameters: https://web.archive.org/web/20221003213817/https://www.tm-forum.com/viewtopic.php?p=154464#p154464

## Configuration

Configuration happens on two `.txt` files which are formatted in XML, name can be anything you like. The dedicated configuration needs to be located in `GameData/Config/` and game settings in `GameData/Tracks/`. 

### Dedicated Server Configuration

Example:

```
<?xml version="1.0" encoding="utf-8" ?>
<dedicated>
    <authorization_levels>
        <level>
            <name>SuperAdmin</name>
            <password>SuperAdmin</password>
        </level>
        <level>
            <name>Admin</name>
            <password>Admin</password>
        </level>
        <level>
            <name>User</name>
            <password>User</password>
        </level>
    </authorization_levels>
 
    <masterserver_account>
        <login></login>
        <password></password>
    </masterserver_account>
 
    <server_options>
        <name></name>
        <comment></comment>
 
        <max_players>32</max_players>
        <password></password>
 
        <max_spectators>32</max_spectators>
        <password_spectator></password_spectator>
 
        <ladder_mode>forced</ladder_mode>     <!-- value between 'inactive', 'forced' (or '0', '1') -->
 
        <enable_p2p_upload>True</enable_p2p_upload>
        <enable_p2p_download>True</enable_p2p_download>
 
        <callvote_timeout>60000</callvote_timeout>
        <callvote_ratio>0.5</callvote_ratio>
 
        <allow_challenge_download>True</allow_challenge_download>
        <autosave_replays>False</autosave_replays>
    </server_options>
 
    <system_config>
        <connection_uploadrate>512</connection_uploadrate>	<!-- KBps -->
        <connection_donwloadrate>8192</connection_donwloadrate>	<!-- KBps -->

        <force_ip_address></force_ip_address>
        <server_port>2350</server_port>
        <server_p2p_port>3450</server_p2p_port>
        <client_port>0</client_port>
        <bind_ip_address></bind_ip_address>
        <use_nat_upnp></use_nat_upnp>
 
        <xmlrpc_port>5000</xmlrpc_port>
        <xmlrpc_allowremote>False</xmlrpc_allowremote>	<!-- If you specify an ip adress here, it'll be the only accepted adress. this will improve security. -->
 
        <blacklist_url></blacklist_url>
        <guestlist_filename></guestlist_filename>
        <blacklist_filename></blacklist_filename>
 
        <use_proxy>False</use_proxy>
        <proxy_login></proxy_login>
        <proxy_password></proxy_password>
    </system_config>
</dedicated>
```


### Game Settings

Example:

```
<?xml version="1.0" encoding="utf-8" ?>
<playlist>
	<gameinfos>
		<game_mode>1</game_mode>
		<chat_time>10000</chat_time>
		<finishtimeout>1</finishtimeout>
		<allwarmupduration>1</allwarmupduration>
		<disablerespawn>0</disablerespawn>
		<forceshowallopponents>0</forceshowallopponents>
		<rounds_pointslimit>30</rounds_pointslimit>
		<rounds_usenewrules>0</rounds_usenewrules>
		<rounds_forcedlaps>0</rounds_forcedlaps>
		<rounds_pointslimitnewrules>5</rounds_pointslimitnewrules>
		<team_pointslimit>50</team_pointslimit>
		<team_maxpoints>6</team_maxpoints>
		<team_usenewrules>0</team_usenewrules>
		<team_pointslimitnewrules>5</team_pointslimitnewrules>
		<timeattack_limit>180000</timeattack_limit>
		<timeattack_synchstartperiod>0</timeattack_synchstartperiod>
		<laps_nblaps>3</laps_nblaps>
		<laps_timelimit>300000</laps_timelimit>
		<cup_pointslimit>100</cup_pointslimit>
		<cup_roundsperchallenge>3</cup_roundsperchallenge>
		<cup_nbwinners>3</cup_nbwinners>
		<cup_warmupduration>2</cup_warmupduration>
	</gameinfos>

	<hotseat>
		<game_mode>0</game_mode>
		<time_limit>300000</time_limit>
		<rounds_count>5</rounds_count>
	</hotseat>

	<filter>
		<is_lan>1</is_lan>
		<is_internet>1</is_internet>
		<is_solo>0</is_solo>
		<is_hotseat>0</is_hotseat>
		<sort_index>1000</sort_index>
		<random_map_order>0</random_map_order>
		<force_default_gamemode>0</force_default_gamemode>
	</filter>

	<startindex>0</startindex>
	<challenge>
		<file>Campaigns\Nations\Blue\C01-Race.Challenge.Gbx</file>
		<ident>eDgWjoKe2dT3GfoTCGCmI_qMvfk</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C02-Race.Challenge.Gbx</file>
		<ident>hlRjJEZGm0yr1sT91CtdIwmqsti</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C03-Acrobatic.Challenge.Gbx</file>
		<ident>c4oQLgleEPkNtehypwdYXTkmVvi</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C04-Race.Challenge.Gbx</file>
		<ident>yWy7ROt2lgk2zL44HKdBgUjuthi</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C05-Endurance.Challenge.Gbx</file>
		<ident>UR7xWwTkMeFB2kqVLVVOGDBCKFb</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C06-Speed.Challenge.Gbx</file>
		<ident>fwj7Gn1nSQ_8qx6MPUtzAfHngTj</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C07-Race.Challenge.Gbx</file>
		<ident>PLVn84D8NoVGjidP1pLafZP8qA8</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C08-Obstacle.Challenge.Gbx</file>
		<ident>Hb_oIOr6Y4_I3aoMogsTPufz8hl</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C09-Race.Challenge.Gbx</file>
		<ident>9MOwoNkpYZhw8e99cxFI3hVZrvi</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C10-Acrobatic.Challenge.Gbx</file>
		<ident>XYiTfAdultrTWVJpjl_Bdnf7x4l</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C11-Race.Challenge.Gbx</file>
		<ident>npRjhClGPZMs_YK_T5yUrnWY0q9</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C12-Obstacle.Challenge.Gbx</file>
		<ident>znbgMZayw8uBByLWqc6kYsEfG6l</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C13-Race.Challenge.Gbx</file>
		<ident>qxHe8iBNC2soNhkOoOvEKDkxZ58</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C14-Endurance.Challenge.Gbx</file>
		<ident>uuGCAivChymPBU6TAHp6qIKSoR4</ident>
	</challenge>
	<challenge>
		<file>Campaigns\Nations\Blue\C15-Speed.Challenge.Gbx</file>
		<ident>n4QZfCzSzwMxsY2ILHFUEEipjtg</ident>
	</challenge>
</playlist>
```

## Deeplink Support

Deeplinking is supported to make your server easier accessable for players. 

`tmtp://#join=IPAddress:Port`

## Testing Rechability of Internetserver

Can be tested on http://dedimania.net/deditest

## Source

More Information about Serverhosting can be aquired on https://server.xaseco.org/

## Game Modes

TBW
