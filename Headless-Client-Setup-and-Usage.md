Starting up a headless client and having it connect to your server is easy, Creating a mission that uses the HC is not. This guide handles the setup and connection ONLY. ***All references to `arma3server` are referring to the script you use to start your server, not the server executable itself unless noted.***  
  
1. Navigate to the directory containing your `arma3server` script. Create a copy of `arma3server` with a new name, in this example we will use `arma3HC`. `cp arma3server arma3HC`  
  
2. Edit your new `arma3HC` with your prefered text editor. You will need to add 12 to the `port=`, 2302 becomes 2314 and so on. Under `params=` you will need to add the following `-client -connect=your.server.ip:port` do not use 127.0.0.1 for the ip. You can remove `-ip=${ip} -netlogs -bepath=${bepath}` Change `servicename="arma3-server"` to `servicename="arma3-HC"`.  
  
3. Navigate to your `cfg` directory. `cd location-of-arma3server-script/serverfiles/cfg` by default. Edit your `arma3-server.server.cfg` with your preferred text editor. Add or edit the lines 
`headlessClient[]={"xxx.xxx.xxx.xxx"};
localClient[]={xxx.xxx.xxx.xxx};
battleyeLicense=1;'  
  
Where xxx.xxx.xxx.xxx is the PUBLIC IP of the server, do not use 127.0.0.1. ***DO NOT USE `localClient[]=` UNLESS THE HEADLESS CLIENT AND SERVER ARE ON THE SAME MACHINE OR LAN***  
  
4. Navigate to your profile directory. By default `cd ~/.local/share/Arma\ 3\ -\ Other\ Profiles` and edit `Player.Arma3Profile` with your preferred text editor to include the line `battleyeLicense=1;`.  
  
5. Start your server with `./arma3server start` Start your headless client with `./arma3HC start`.  
  
Only a logged in admin can see the headless clients in the player menu on the server. The headless client will connect and automatically assume the first available headless client slot. ***In version 1.62 the PBO signature detection for headless clients is broken on linux, they will be kicked by the server. This is fixed in the dev branch update 1.65.138087.***