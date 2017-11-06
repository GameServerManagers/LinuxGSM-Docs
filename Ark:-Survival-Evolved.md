Best guide to install: 

https://gameservermanagers.com/lgsm/arkserver/

FAQ: 

Q: How do you change ark server settings?
A: /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
and
/home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
-----
Q: How do you change the map?
A: I recommend following this video tutorial:
https://www.youtube.com/watch?v=wJr0Vrnveas
-----
Q: How do you add mods to the server?
A: Go to /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
then under [ServerSettings] add this line: 
ActiveMods=ID1,ID2,ID3
Replace "ID" with your workshop ID's.
After that, move your downloaded mods folders and .mod files to
/home/arkserver/serverfiles/ShooterGame/Content/Mods/
-----
Q: How do you know if your ark server is working? 
A: In console, run "./arkserver console".
If you are still unsure, run:
netstat -tulpn | grep ShooterGameSe
Your results should look something like this:
udp        0      0 0.0.0.0:27015           0.0.0.0:*                           23440/ShooterGameSe
udp        0      0 0.0.0.0:7778            0.0.0.0:*                           23440/ShooterGameSe
tcp        0      0 0.0.0.0:32330           0.0.0.0:*               LISTEN      23440/ShooterGameSe

If you only have one result, then the server is not fully running.
-----
Q: How do I access logs?
A: /home/arkserver/log/server/ShooterGame.log
   /home/arkserver/log/console/arkserver-console.log
   /home/arkserver/log/script/arkserver-script.log
-----
Q: How do I have multiple instances on one server?
A: https://github.com/GameServerManagers/LinuxGSM/wiki/Multiple-Game-Servers
-----
Q: How to automatically restart the server? (When it crashes, etc)
A: Run ./arkserver monitor
-----
Q: How to backup the server?
A: Run ./arkserver backup
-----