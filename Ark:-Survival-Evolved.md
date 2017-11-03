Best guide to install : 

https://gameservermanagers.com/lgsm/arkserver/

FAQ : 

Q : How to change serveur ARK settings ?

R : go to the files : 

         U have two files to modifie : (for details go ark survival docs here --> Add it)
         nano /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini
         and
         nano /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/Game.ini
                  Exemple of files i using : 
                           GameUserSettings.ini ---> Add it
                           Game.ini ---> Add it
-----
Q : How to change map (Official MAP)?

R : To change map : 

         Modifie files : 

         nano /home/arkserver/lgsm/config-lgsm/arkserver/common.cfg

         add this : https://gist.github.com/gamersalpha/fee10317b768e3f7ada8186a4045df21

         and just change the name of the map : 
                  ...
                  parms=Ragnarok?
                  ...

         u can choose with official map :
         Ragnarok
         TheIsland

-----
Q : How to add mods on the serveur ?

          R : 
          nano /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini

          in [ServerSettings] add this line : 
                    ActiveMods=835113702,679529026,764755314,609380111,639841665,558079412,731604991,768494420ls 

/home/arkserver/Steam/steamapps/workshop/content/346110/

/home/arkserver/serverfiles/ShooterGame/Content/Mods/


-----
Q : how to know u server ARK is really ready to play : 
          R : lunch this command and if u have the same result is OK, only one line and u have to wait
root@server:~# netstat -tulpn | grep ShooterGameSe
udp        0      0 0.0.0.0:27015           0.0.0.0:*                           23440/ShooterGameSe
udp        0      0 0.0.0.0:7778            0.0.0.0:*                           23440/ShooterGameSe
tcp        0      0 0.0.0.0:32330           0.0.0.0:*               LISTEN      23440/ShooterGameSe

          and do : 

          ./arkserver u


-----
Q : How to change map (not Official MAP)?

R : looking for


-----
Q : Afficher des logs ?

          R :  tail -f /home/arkserver/log/server/ShooterGame.log
               tail -f /home/arkserver/log/console/arkserver-console.log
               tail -f /home/arkserver/log/script/arkserver-script.log

-----

Q : How to have to instance server on the same server ?


        R : found here --> https://github.com/GameServerManagers/LinuxGSM/wiki/Multiple-Game-Servers


-----

Q : How create a service for linux-gsm, and start my ark serveur automaticly when crashed or restart server ?

        R : 
-----

Q : How make a backup external ?

        R : 
-----

Q : How to restore an old backup ? 

        R : 
                SpaceCat? - Aujourd'hui à 00:16

                Backup shuts down the server, and compresses the root folder of the server instance.

                and starts the server back up. Depending on the mods, it can get quite bulky.

                I have a side project I need to start to try and reduce the size of backups

-----

Q : Rcon - I want create a php interface for it ? i found some code working in command line, now i have to make PHP page to interface it

        R : 




