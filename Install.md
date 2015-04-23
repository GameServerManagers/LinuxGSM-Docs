Below are the basic instructions to get started with installing a game server using LGSM.
Select the server you want to install and follow the instructions.

> note: Ensure you have installed the relevant [[dependencies]] before you install a server

### Game Servers
 - [7 Days to Die](#7-Day-to-Die)
 - [ARMA 3](#ARMA-3)
 - [Blade Symphony](#Blade-Symphony)
 - [Counter-Strike 1.6](#Counter-Strike-1.6)
 - [Counter-Strike: Condition Zero](#Counter-Strike-Condition-Zero)
 - [Counter-Strike: Global Offensive](#Counter-Strike-Global-Offensive)
 - [Counter-Strike: Source](#Counter-Strike-Global-Offensive)
 - [Day of Defeat](#Day-of-Defeat)
 - [Day of Defeat: Source](#Day-of-Defeat-Source)
 - [Deathmatch Classic](#Day-of-Defeat-Source)
 - [Double Action: Boogaloo](#Double-Action-Boogaloo)
 - [Fistful of Frags](#Fistful-of-Frags)
 - [Garry's Mod](#Garrys-Mod)
 - [Half Life: Deathmatch](#Half-Life-Deathmatch)
 - [Half Life 2: Deathmatch](#Half-Life-202-Deathmatch)
 - [Insurgency](#Insurgency)
 - [Just Cause 2](#Just-Cause-2)
 - [Killing Floor](#Killing-Floor)
 - [Left 4 Dead](#Left-4-Dead)
 - [Left 4 Dead 2](#Left-4-Dead)
 - [Mumble](#Mumble)
 - [No More Room in Hell](#No-More-Room-in-Hell)
 - [Natural Selection 2](#Natural-Selection-2)
 - [NS2: Combat](#NS2-Combat)
 - [Opposing Force](#Opposing-Force)
 - [Project Zomboid](#ProjectZomboid)
 - [Red Orchestra: Ostfront 41-45](#Red-Orchestra-Ostfront-41-45)
 - [Ricochet](#Ricochet)
 - [Serious Sam 3: BFE](#Serious-Sam-3-BFE)
 - [Starbound](#Starbound)
 - [Team Fortress 2](#Team-Fortress-2)
 - [Team Fortress Classic](#Team-Fortress-Classic)
 - [Teamspeak 3](#Teamspeak-3)
 - [Unreal Tournament 2004](#Unreal-Tournament-2004)
 - [Unreal Tournament 99](#Unreal-Tournament-99)

# <a name="7-Day-to-Die"></a>7 Days to Die
![7 Days to Die](http://cdn.akamai.steamstatic.com/steam/apps/251570/header.jpg)

1. Create a user and login.

        adduser sdtdserver
        passwd sdtdserver
        su - sdtdserver

2. Download the script. `wget http://gameservermanagers.com/dl/sdtdserver`
3. Make it executable. `chmod +x sdtdserver`
4. Add Steam login details. `nano sdtdserver`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./sdtdserver install

# <a name="ARMA-3"></a>ARMA 3
![ARMA 3](http://cdn.akamai.steamstatic.com/steam/apps/107410/header.jpg)

1. Create a user and login.

        adduser arma3server
        passwd arma3server
        su - arma3server

2. Download the script. `wget http://gameservermanagers.com/dl/arma3server`
3. Make it executable. `chmod +x arma3server`
4. Add Steam login details. `nano arma3server`

> You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

    # Steam login
    steamuser="username"
    steampass="password"
5. Run the installer and follow the instructions.

    ./arma3server install

# <a name="Blade-Symphony"></a>Blade Symphony
![Blade Symphony](http://cdn.akamai.steamstatic.com/steam/apps/225600/header.jpg)

> note: You must own a copy of this game in a steam account to download the server.

1. Create a user and login.

        adduser bsserver
        passwd bsserver
        su - bsserver

2. Download the script. `wget http://gameservermanagers.com/dl/bsserver`
3. Make it executable. `chmod +x bsserver`
4. Add Steam login details. `nano bsserver`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./bsserver install

# <a name="Counter-Strike-1.6"></a>Counter-Strike 1.6
![Counter-Strike 1.6](http://cdn.akamai.steamstatic.com/steam/apps/10/header.jpg)

1. Create a user and login.

        adduser csserver
        passwd csserver
        su - csserver
2. Download the script. `wget http://gameservermanagers.com/dl/csserver`
3. Make it executable. `chmod +x csserver`
4. Run the installer and follow the instructions.

        ./csserver install

# <a name="Counter-Strike-Condition-Zero"></a>Counter-Strike: Condition Zero
![Counter-Strike: Condition Zero](http://cdn.akamai.steamstatic.com/steam/apps/80/header.jpg)

1. Create a user and login.

        adduser csczserver
        passwd csczserver
        su - csczserver
2. Download the script. `wget http://gameservermanagers.com/dl/csczserver`
3. Make it executable. `chmod +x csczserver`
4. Run the installer and follow the instructions.

        ./csczserver install

# <a name="Counter-Strike-Global-Offensive"></a>Counter-Strike: Global Offensive
![Counter-Strike: Global Offensive](http://cdn.akamai.steamstatic.com/steam/apps/730/header.jpg)

1. Create a user and login.

        adduser csgoserver
        passwd csgoserver
        su - csgoserver
2. Download the script. `wget http://gameservermanagers.com/dl/csgoserver`
3. Make it executable. `chmod +x csgoserver`
4. Run the installer and follow the instructions.

        ./csgoserver install

# <a name="Counter-Strike-Source"></a>Counter-Strike: Source
![Counter-Strike: Source](http://cdn.akamai.steamstatic.com/steam/apps/240/header.jpg)

1. Create a user and login.

        adduser cssserver
        passwd cssserver
        su - cssserver
2. Download the script. `wget http://gameservermanagers.com/dl/cssserver`
3. Make it executable. `chmod +x cssserver`
4. Run the installer and follow the instructions.

        ./cssserver install

# <a name="Day-of-Defeat"></a>Day of Defeat
![Day of Defeat](http://cdn.akamai.steamstatic.com/steam/apps/30/header.jpg)

1. Create a user and login.

        adduser dodserver
        passwd dodserver
        su - dodserver
2. Download the script. `wget http://gameservermanagers.com/dl/dodserver`
3. Make it executable. `chmod +x dodserver`
4. Run the installer and follow the instructions.

        ./dodserver install

# <a name="Day-of-Defeat-Source"></a>Day of Defeat: Source
![Day of Defeat: Source](http://cdn.akamai.steamstatic.com/steam/apps/300/header.jpg)

1. Create a user and login.

        adduser dodsserver
        passwd dodsserver
        su - dodsserver
2. Download the script. `wget http://gameservermanagers.com/dl/dodsserver`
3. Make it executable. `chmod +x dodsserver`
4. Run the installer and follow the instructions.

        ./dodsserver install

# <a name="Deathmatch-Classic"></a>Deathmatch Classic
![Deathmatch Classic](http://cdn.akamai.steamstatic.com/steam/apps/40/header.jpg)

1. Create a user and login.

        adduser dmcserver
        passwd dmcserver
        su - dmcserver
2. Download the script. `wget http://gameservermanagers.com/dl/dmcserver`
3. Make it executable. `chmod +x dmcserver`
4. Run the installer and follow the instructions.

        ./dmcserver install

# <a name="Double-Action-Boogaloo"></a>Double Action: Boogaloo
![Double Action: Boogaloo](http://cdn.akamai.steamstatic.com/steam/apps/317360/header.jpg)

1. Create a user and login.

        adduser dabserver
        passwd dabserver
        su - dabserver
2. Download the script. `wget http://gameservermanagers.com/dl/dabserver`
3. Make it executable. `chmod +x dabserver`
4. Run the installer and follow the instructions.

        ./dabserver install

# <a name="Fistful-of-Frags"></a>Fistful of Frags
![Fistful of Frags](http://cdn.akamai.steamstatic.com/steam/apps/265630/header.jpg)

1. Create a user and login.

        adduser fofserver
        passwd fofserver
        su - fofserver
2. Download the script. `wget http://gameservermanagers.com/dl/fofserver`
3. Make it executable. `chmod +x fofserver`
4. Run the installer and follow the instructions.

        ./fofserver install

# <a name="Garrys-Mod"></a>Garry's Mod
![Garry's Mod](http://cdn.akamai.steamstatic.com/steam/apps/4000/header.jpg)

1. Create a user and login.

        adduser gmodserver
        passwd gmodserver
        su - gmodserver
2. Download the script. `wget http://gameservermanagers.com/dl/gmodserver`
3. Make it executable. `chmod +x gmodserver`
4. Run the installer and follow the instructions.

        ./gmodserver install

# <a name="Half-Life-Deathmatch"></a>Half Life: Deathmatch
![Half Life: Deathmatch](http://cdn.akamai.steamstatic.com/steam/apps/70/header.jpg)

1. Create a user and login.

        adduser hldmserver
        passwd hldmserver
        su - hldmserver
2. Download the script. `wget http://gameservermanagers.com/dl/hldmserver`
3. Make it executable. `chmod +x hldmserver`
4. Run the installer and follow the instructions.

        ./hldmserver install

# <a name="Half-Life-2-Deathmatch"></a>Half Life 2: Deathmatch
![Half Life 2: Deathmatch](http://cdn.akamai.steamstatic.com/steam/apps/320/header.jpg)

1. Create a user and login.

        adduser hl2dmserver
        passwd hl2dmserver
        su - hl2dmserver
2. Download the script. `wget http://gameservermanagers.com/dl/hl2dmserver`
3. Make it executable. `chmod +x hl2dmserver`
4. Run the installer and follow the instructions.

        ./hl2dmserver install

# <a name="Insurgency"></a>Insurgency
![Insurgency](http://cdn.akamai.steamstatic.com/steam/apps/222880/header.jpg)

1. Create a user and login.

        adduser insserver
        passwd insserver
        su - insserver
2. Download the script. `wget http://gameservermanagers.com/dl/insserver`
3. Make it executable. `chmod +x insserver`
4. Run the installer and follow the instructions.

        ./insserver install

# <a name="Just-Cause-2"></a>Just Cause 2
![Just Cause 2](http://cdn.akamai.steamstatic.com/steam/apps/8190/header.jpg)

1. Create a user and login.

        adduser jc2server
        passwd jc2server
        su - jc2server
2. Download the script. `wget http://gameservermanagers.com/dl/jc2server`
3. Make it executable. `chmod +x jc2server`
4. Run the installer and follow the instructions.

        ./jc2server install

# <a name="Killing-Floor"></a>Killing Floor
![Killing Floor](http://cdn.akamai.steamstatic.com/steam/apps/1250/header.jpg)

1. Create a user and login.

        adduser kfserver
        passwd kfserver
        su - kfserver
2. Download the script. `wget http://gameservermanagers.com/dl/kfserver`
3. Make it executable. `chmod +x kfserver`
4. Add Steam login details. `nano kfserver`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./kfserver install

# <a name="Left-4-Dead"></a>Left 4 Dead
![Left 4 Dead](http://cdn.akamai.steamstatic.com/steam/apps/500/header.jpg)

1. Create a user and login.

        adduser l4dserver
        passwd l4dserver
        su - l4dserver
2. Download the script. `wget http://gameservermanagers.com/dl/l4dserver`
3. Make it executable. `chmod +x l4dserver`
4. Run the installer and follow the instructions.

        ./l4dserver install

# <a name="Left-4-Dead-2"></a>Left 4 Dead 2
![Left 4 Dead 2](http://cdn.akamai.steamstatic.com/steam/apps/550/header.jpg)

1. Create a user and login.

        adduser l4d2server
        passwd l4d2server
        su - l4d2server
2. Download the script. `wget http://gameservermanagers.com/dl/l4d2server`
3. Make it executable. `chmod +x l4d2server`
4. Run the installer and follow the instructions.

        ./l4d2server install

# <a name="Mumble"></a>Mumble
![Mumble](http://gameservermanagers.com/wp-content/themes/lgsm/img/games/mumbleserver_logo-250x143.jpg)

1. Create a user and login.
        adduser mumbleserver
        passwd mumbleserver

        su - mumbleserver
2. Download the script.
    `wget http://gameservermanagers.com/dl/mumbleserver`
3. Make it executable.
    `chmod +x mumbleserver`
4. Run the installer and follow the instructions.

        ./mumbleserver install

# <a name="No-More-Room-in-Hell"></a>No More Room in Hell
![No More Room in Hell](http://cdn.akamai.steamstatic.com/steam/apps/224260/header.jpg)

1. Create a user and login.

        adduser nmrihserver
        passwd nmrihserver
        su - nmrihserver
2. Download the script. `wget http://gameservermanagers.com/dl/nmrihserver`
3. Make it executable. `chmod +x nmrihserver`
4. Add Steam login details. `nano nmrihserver`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./nmrihserver install

# <a name="Natural-Selection-2"></a>Natural Selection 2
![Natural Selection 2](http://cdn.akamai.steamstatic.com/steam/apps/4920/header.jpg)

1. Create a user and login.

        adduser ns2server
        passwd ns2server
        su - ns2server
2. Download the script. `wget http://gameservermanagers.com/dl/ns2server`
3. Make it executable. `chmod +x ns2server`
4. Add Steam login details. `nano ns2server`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./ns2server install

# <a name="Opposing-Force"></a>Opposing Force
![Opposing Force](http://cdn.akamai.steamstatic.com/steam/apps/50/header.jpg)

1. Create a user and login.

        adduser opforserver
        passwd opforserver
        su - opforserver
2. Download the script.
    `wget http://gameservermanagers.com/dl/opforserver`
3. Make it executable.
    `chmod +x opforserver`
4. Run the installer and follow the instructions.

        ./opforserver install

# <a name="ProjectZomboid"></a>Project Zomboid
![Project Zomboid](http://cdn.akamai.steamstatic.com/steam/apps/108600/header.jpg)

1. Create a user and login.

        adduser pzserver
        passwd pzserver
        su - pzserver
2. Download the script.
    `wget http://gameservermanagers.com/dl/pzserver`
3. Make it executable.
    `chmod +x pzserver`
4. Run the installer and follow the instructions.

        ./pzserver install

# <a name="Red-Orchestra-Ostfront-41-45"></a>Red Orchestra: Ostfront 41-45
![Red Orchestra: Ostfront 41-45](http://cdn.akamai.steamstatic.com/steam/apps/1200/header.jpg)

1. Create a user and login.

        adduser roserver
        passwd roserver
        su - roserver
2. Download the script. `wget http://gameservermanagers.com/dl/roserver`
3. Make it executable. `chmod +x roserver`
4. Add Steam login details. `nano roserver`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./roserver install

# <a name="Ricochet"></a>Ricochet
![Ricochet](http://cdn.akamai.steamstatic.com/steam/apps/60/header.jpg)

1. Create a user and login.
        adduser ricochetserver
        passwd ricochetserver

        su - ricochetserver
2. Download the script.
    `wget http://gameservermanagers.com/dl/ricochetserver`
3. Make it executable.
    `chmod +x ricochetserver`
4. Run the installer and follow the instructions.

        ./ricochetserver install

# <a name="Serious-Sam-3-BFE"></a>Serious Sam 3: BFE
![Red Orchestra: Ostfront 41-45](http://cdn.akamai.steamstatic.com/steam/apps/41070/header.jpg)

1. Create a user and login.

        adduser ss3server
        passwd ss3server
        su - ss3server
2. Download the script. `wget http://gameservermanagers.com/dl/ss3server`
3. Make it executable. `chmod +x ss3server`
4. Add Steam login details. `nano ss3server`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./ss3server install

# <a name="Starbound"></a>Starbound
![Starbound](http://cdn.akamai.steamstatic.com/steam/apps/211820/header.jpg)

> note: You must own a copy of this game in a steam account to download the server.

1. Create a user and login.

        adduser sbserver
        passwd sbserver
        su - sbserver

2. Download the script. `wget http://gameservermanagers.com/dl/sbserver`
3. Make it executable. `chmod +x sbserver`
4. Add Steam login details. `nano sbserver`

    > You will need to enter your steam username and password to allow authentication to the SteamCMD system. I recommend that you create a new Steam username just for the server.

        # Steam login
        steamuser="username"
        steampass="password"

5. Run the installer and follow the instructions.

        ./sbserver install

# <a name="Team-Fortress-2"></a>Team Fortress 2
![Team Fortress 2](http://cdn.akamai.steamstatic.com/steam/apps/440/header.jpg)

1. Create a user and login.

        adduser tf2server
        passwd tf2server
        su - tf2server
2. Download the script.
    `wget http://gameservermanagers.com/dl/tf2server`
3. Make it executable.
    `chmod +x tf2server`
4. Run the installer and follow the instructions.

        ./tf2server install

# <a name="Team-Fortress-Classic"></a>Team Fortress Classic
![Team Fortress Classic](http://cdn.akamai.steamstatic.com/steam/apps/20/header.jpg)

1. Create a user and login.

        adduser tfcserver
        passwd tfcserver
        su - tfcserver
2. Download the script.
    `wget http://gameservermanagers.com/dl/tfcserver`
3. Make it executable.
    `chmod +x tfcserver`
4. Run the installer and follow the instructions.

        ./tfcserver install

# <a name="Teamspeak-3"></a>Teamspeak 3
![Teamspeak 3](http://gameservermanagers.com/wp-content/themes/lgsm/img/games/ts3server_logo-250x143.jpg)

1. Create a user and login.

        adduser ts3server
        passwd ts3server
        su - ts3server
2. Download the script.
    `wget http://gameservermanagers.com/dl/ts3server`
3. Make it executable.
    `chmod +x ts3server`
4. Run the installer and follow the instructions.

        ./ts3server install

# <a name="Unreal-Tournament-2004"></a>Unreal Tournament 2004
![Unreal Tournament 2004](http://cdn.akamai.steamstatic.com/steam/apps/13230/header.jpg)

1. Create a user and login.

        adduser ut2k4server
        passwd ut2k4server
        su - ut2k4server
2. Download the script.
    `wget http://gameservermanagers.com/dl/ut2k4server`
3. Make it executable.
    `chmod +x ut2k4server`
4. Run the installer and follow the instructions.

        ./ut2k4server install

# <a name="Unreal-Tournament-99"></a>Unreal Tournament 99
![Unreal Tournament 2004](http://cdn.akamai.steamstatic.com/steam/apps/13240/header.jpg)

1. Create a user and login.

        adduser ut99server
        passwd ut99server
        su - ut99server
2. Download the script.
    `wget http://gameservermanagers.com/dl/ut99server`
3. Make it executable.
    `chmod +x ut99server`
4. Run the installer and follow the instructions.

        ./ut99server install
