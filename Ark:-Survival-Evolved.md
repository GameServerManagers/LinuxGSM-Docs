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

Q : How to add mods on the serveur ?

          R : 
          nano /home/arkserver/serverfiles/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini

          in [ServerSettings] add this line : 
                    ActiveMods=835113702,679529026,764755314,609380111,639841665,558079412,731604991,768494420

          and do : 

          ./arkserver u


Q : How to change map (not Official MAP)?

R : looking for

Q : Afficher des logs ?

          R :  tail -f /home/arkserver/log/server/ShooterGame.log
               tail -f /home/arkserver/log/console/arkserver-console.log
               tail -f /home/arkserver/log/script/arkserver-script.log




...






