# Unreal Tournament 3

## Server files

LinuxGSM uses the most recent version of UT3 server available for Linux

> v2.1 \(3808\) \[Compiled: Apr 22 2009 04:27:51\].

This update includes the TitanPack DLC.

## Ports

* Game Port 7777 UDP handled by Parms
* Query port 6500 UDP handled by parms \(does not work\)
* Web Admin 8080 TCP handled by UTWeb.ini

## Running a dedicated server

The basic format of running server start command line is:-

```text
UT3.exe Server <map>?<variable1>=<value1>?<variable2>=<value2>.... -login=<login> -password=<password> -unattended

```

Examples of this would be:-

```text
UT3.exe Server DM-ShangriLa?game=UTGame.UTDuelGame -login=<login> -password=<password> -unattended

UT3.exe Server VCTF-Suspense -login=<login> -password=<password> -unattended

```

NOTE: To launch multiple servers on a machine you must use the ut3.exe binary, not the ut3.com binary. The result of using the .com was, among others, the inability to stop a single instance without killing all the running instances.\[[edit](http://wiki.unrealadmin.org/index.php?title=FAQ:UT3&action=edit&section=2)\]

### **Game Types & Mutators**

This is a list of the valid gametypes:

| Name | GameType |
| :--- | :--- |
| Deathmatch | UTGame.UTDeathmatch |
| Capture the Flag | UTGameContent.UTCTFGame\_Content |
| Warfare | UTGameContent.UTOnslaughtGame\_Content |
| Vehicle Capture the Flag | UTGameContent.UTVehicleCTFGame\_Content |
| Team Deathmatch | UTGame.UTTeamGame |
| Duel | UTGame.UTDuelGame |

For mutators you need to set the variable of each mutator:-

1. Mutator=&lt;MutatorIdentifier&gt;

Here is a list of Mutators shipped with the Retail Version:

| Name | MutatorIdentifier |
| :--- | :--- |
| Instagib | UTGame.UTMutator\_Instagib |
| BigHead | UTGame.UTMutator\_BigHead |
| Low Gravity | UTGame.UTMutator\_LowGrav |
| Super Berserk | UTGame.UTMutator\_SuperBerserk |
| Friendly Fire | UTGame.UTMutator\_FriendlyFire |
| No Translocator | UTGame.UTMutator\_NoTranslocator |
| Speed Freak | UTGame.UTMutator\_SpeedFreak |
| Handicap | UTGame.UTMutator\_Handicap |
| No Powerups | UTGame.UTMutator\_NoPowerups |
| Slomo | UTGame.UTMutator\_Slomo |
| Weapon Replacement | UTGame.UTMutator\_WeaponReplacement |
| Weapon Respawn | UTGame.UTMutator\_WeaponsRespawn |

if you want to run more than one mutator separate them with commas:

```text
 ?mutator=UTGame.UTMutator_Instagib,UTGame.UTMutator_LowGrav
```

\[[edit](http://wiki.unrealadmin.org/index.php?title=FAQ:UT3&action=edit&section=3)\]

### **Common Variables**

* MaxPlayers=&lt;number&gt; Maximum number of players on the server \(overrides ini setting\)
* MinNetPlayers=&lt;number&gt; Minimum number of players before a match starts \(real players not bots\)
* bShouldAdvertise=\[True\|False\] Show the server in the server browser \(default: true\)
* bIsLanMatch=\[True\|False\] Is this a LAN only game? \(default: false\)
* bIsDedicated=\[True\|False\] Changes dedicated server flag \(default: false, even if started as dedicated\)
* GamePassword=&lt;password&gt; Sets a game password
* AdminPassword=&lt;password&gt; Sets an admin password
* Port=&lt;port&gt; Sets the server game port \(default: 7777; can also be changed via the INI file\)
* QueryPort=&lt;port&gt; Sets the server query port \(default: 6500\)
* GoalScore=&lt;number&gt; Sets the max frags / max caps before the server will change maps.
* bUsesStats=\[True\|False\] Report stats or not?
* TimeLimit=&lt;number&gt; Sets the timelimit in minutes for each map.

Most of these can be set in the server's INI file, so there's no need to clutter up the command line.\[[edit](http://wiki.unrealadmin.org/index.php?title=FAQ:UT3&action=edit&section=4)\]

### **Running Behind a Router/Firewall**

1. Setup port forwarding for three ports \(all UDP only\): 13000, 7777 and 6500 \(or whatever port/queryport your server is running on; 7777/6500 are the defaults\).

### **Server Logins**

ATM all servers need a **unique** login, as in no two servers can use the same login. Doing so will mean that one of those servers will not show in the list. This login has to be created via the client "Create Profile". You can create multiple profiles under the same email address but you must use the same password for each if you do so.\[[edit](http://wiki.unrealadmin.org/index.php?title=FAQ:UT3&action=edit&section=6)\]

### **Query Protocol**

The server uses the GameSpy query Protocol \( v4 \) which can be queried with qstat e.g.

```text
qstat -R -gs4 <ip>:<port>
```

#### **Notes**

* If you want the map you must currently request server rules with -R as the server doesnt currently return the map in the basic query.

For more details about the query protocol \(including the PHP code to do web-based querying and details on the query variables\) check out the [UT3\_query\_protocol](http://wiki.unrealadmin.org/UT3_query_protocol) page.

### **Multiple Servers on One Machine**

Each server process needs to run under a different gamespy account \(can be created in the game\). Important things to note are:

* The `-nohomedir` command forces the servers to use the install directory instead of My Documents...
* The `-configsubdir=<serverfoldername>` will create a folder under `..\UTGame\config\` so each server instance can have it's own ini files
* `-login=<login>` and `-password=<password>` as these must be unique
* The servers port is changed with `-Port=<port>` in the URL, or via the setting in `UTEngine.ini`
* The servers query port is changed with -QueryPort=&lt;port&gt;
* You must specify -unattended as without it you will get prompted to confirm the upgrade of the server's configuration files. This option needs to be last in the command line.

Note: `-configsubdir=` does not work unless `-nohomedir` is specified.

### **Server Names**

Server names can be specified in the server's INI file, as of patch 1.1.

The ServerDescription field isn't in plain ascii or text as you and I know it. Instead its in UCS2 aka UTF-16 which is then serialized as numeric strings. It is possible to generate the server description code here: \[[Cruz's UT3 Server Description Generator](http://www.penetrate.nl/UT3ServerDesc.php)\]\[[edit](http://wiki.unrealadmin.org/index.php?title=FAQ:UT3&action=edit&section=9)\]

### **Enable Mapvote**

Edit the ...\UTGame\Config\UTGame.ini. Under the \[UTGame.UTGame\] section, be sure to have this:

```text
bAllowMapVoting=True
VoteDuration=45
GameSpecificMapCycles=(GameClassName="UTDeathmatch",Maps=("DM-Arsenal","DM-Biohazard","DM-CarbonFire","DM-Deck","DM-Defiance","DM-Deimos","DM-Diesel","DM-Fearless","DM-Gateway","DM-HeatRay","DM-RisingSun","DM-Sanctuary","DM-Sentinel","DM-ShangriLa"))
GameSpecificMapCycles=(GameClassName="UTTeamGame",Maps=("DM-Arsenal","DM-Biohazard","DM-CarbonFire","DM-Deck","DM-Defiance","DM-Deimos","DM-Diesel","DM-Fearless","DM-Gateway","DM-HeatRay","DM-RisingSun","DM-Sanctuary","DM-Sentinel","DM-ShangriLa"))
GameSpecificMapCycles=(GameClassName="UTCTFGame_Content",Maps=("CTF-Coret","CTF-Hydrosis","CTF-Reflection","CTF-Vertebrae","CTF-OmicronDawn","CTF-Strident"))
GameSpecificMapCycles=(GameClassName="UTVehicleCTFGame_Content",Maps=("VCTF-Containment","VCTF-Corruption","VCTF-Kargo","VCTF-Necropolis","VCTF-Sandstorm","VCTF-Suspense"))
GameSpecificMapCycles=(GameClassName="UTOnslaughtGame_Content",Maps=("WAR-Avalanche","WAR-Downtown","WAR-Dusk","WAR-FloodGate","WAR-Islander","WAR-Islander_Necris","WAR-MarketDistrict","WAR-OnyxCoast","WAR-Powersurge","WAR-Serenity","WAR-Serenity_Necris","WAR-SinkHole","WAR-TankCrossing","WAR-Torlan","WAR-Torlan_Leviathan","WAR-Torlan_Necris"))
GameSpecificMapCycles=(GameClassName="UTDuelGame",Maps=("DM-Arsenal","DM-Biohazard","DM-CarbonFire","DM-Deck","DM-Defiance","DM-Deimos","DM-Diesel","DM-Fearless","DM-Gateway","DM-HeatRay","DM-RisingSun","DM-Sanctuary","DM-Sentinel","DM-ShangriLa"))
```

### **Admin Commands**

You ment to be able to admin the game using rcon but when we tried it although adminlogin worked none of the subsiquent commands did.

First off login with: AdminLogin &lt;password&gt;

The you can use the following command:

* AdminLogin &lt;password&gt; - Logs you in as an admin
* AdminLogout - Logs you out of admin mode
* AdminRestartMap - Restarts the current map
* AdminChangeMap &lt;MapName&gt; - Loads a different map \(gametype will change too, depending on map\)
* Admin addbots &lt;\#&gt; - Adds number of bots
* Admin killbots - Removes all bots
* AdminPlayerList - Shows PlayerID of players
* Adminkick &lt;playername&gt; - Kicks player from current game
* Adminkickban &lt;playername&gt; - Kicks player from current game and bans player from reconnecting \(bans are stored in .ini file for later editing\)
* AdminForceVoiceMute &lt;playername&gt; - Blocks a player from sending voip to others
* AdminForceVoiceUnMute &lt;playername&gt; - Allows a player to resume sending voip to others
* AdminForceTextMute &lt;playername&gt; - Blocks a player from sending text to others
* AdminForceTextUnMute &lt;playername&gt; - Allows a player to resume sending text to others
* AdminPublishMapList - Overrides the server's map list for the current game type with the one on the client that used the command

When your done you can logout with: AdminLogout

