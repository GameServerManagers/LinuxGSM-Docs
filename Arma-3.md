# Headless Client Setup and Usage
## Headless Client Overview
* Headless Client is used to offload AI calculations from the server.
* Headless Client is integrated into game client and dedicated server executable (Windows and Linux, use -client parameter).
* The server doesn't allow arbitrary connections from headless clients if you do not define the headless clients IPs in the server.cfg.

https://community.bistudio.com/wiki/Arma_3_Headless_Client
Starting up a headless client and having it connect to your server is easy, Creating a mission that uses the HC is not. This guide handles the setup and connection ONLY. ***All references to `arma3server` are referring to the script you use to start your server, not the server executable itself unless noted.***  
  
0. Have LGSM create a new instance script for you: `./linuxgsm.sh arma3server`. Then edit the config under `lgsm/config-lgsm/` you will want to edit the `[instance].cfg` (As of 2017-11. The rest of these instructions below may also need updating.)

1. Navigate to the directory containing your `arma3server` script. Create a copy of `arma3server` with a new name, in this example we will use `arma3HC`. `cp arma3server arma3HC`  
  
2. Edit your new `arma3HC` with your prefered text editor. You will need to add 12 to the `port=`, 2302 becomes 2314 and so on. Under `params=` you will need to add the following `-client -connect=your.server.ip:port` do not use 127.0.0.1 for the ip. You can remove `-ip=${ip} -netlogs -bepath=${bepath}` Change `servicename="arma3-server"` to `servicename="arma3-HC"`.  
  
3. Navigate to your `cfg` directory. `cd location-of-arma3server-script/serverfiles/cfg` by default. Edit your `arma3-server.server.cfg` with your preferred text editor. Add or edit the lines 
`headlessClient[]={"xxx.xxx.xxx.xxx"};  
localClient[]={xxx.xxx.xxx.xxx};  
battleyeLicense=1;`  
  
Where xxx.xxx.xxx.xxx is the PUBLIC IP of the server, do not use 127.0.0.1. ***DO NOT USE `localClient[]=` UNLESS THE HEADLESS CLIENT AND SERVER ARE ON THE SAME MACHINE OR LAN***  
  
4. Navigate to your profile directory. By default `cd ~/.local/share/Arma\ 3\ -\ Other\ Profiles` and edit `Player.Arma3Profile` with your preferred text editor to include the line `battleyeLicense=1;`.  
  
5. Start your server with `./arma3server start` Start your headless client with `./arma3HC start`.  
  
Only a logged in admin can see the headless clients in the player menu on the server. The headless client will connect and automatically assume the first available headless client slot. ***In version 1.62 the PBO signature detection for headless clients is broken on linux, they will be kicked by the server. This is fixed in the dev branch update 1.65.138087. https://twitter.com/FoltynD/status/769181447907311616 ***

# Loading mods
Incorporating mods into the server is not supported by LGSM.  The following guide is a general process for getting modules to load with your server.  However, issues loading modules should be taken up with the mod developers.

For a standard deployment, you will want to have your modules unpacked under `serverfiles/mods`.  For example, your directory structure might have the following raw modules unpacked under `serverfiles/mods`:
```
[arma3server@localhost mods]$ ls 
@ace @AdvancedTowing @CBA_A3 @RHSUSAF @AdvancedRappelling @AdvancedUrbanRappelling @RHSAFRF @AdvancedSlingLoading @Ares @RHSGREF
```
The issue that makes this difficult is that, for some bizarre reason, the server demands that the modules possess all lowercase names.  The following code segments (run from the `serverfiles/mods` directory *as the arma3server user*) change all files and folders to lowercase:
```
depth=0
for x in $(find . -type d | sed "s/[^/]//g")
do
if [ ${depth} -lt ${#x} ]
then 
   let depth=${#x}
fi
done
echo "the depth is ${depth}"
```
As a sanity check here, you should get a depth of 4 or so.  Proceed to iteratively rename the files and directory structure with this code snippet (once again, run from the `serverfiles/mods` directory as the arma3server user):
```
for ((i=1;i<=${depth};i++))
do
  for x in $(find . -maxdepth $i | grep [A-Z])
  do 
    mv $x $(echo $x | tr 'A-Z' 'a-z')
  done
done
```
Now a simple directory listing should at least confirm the top-level folders have all been adjusted:
```
arma3server@gamebox3:~/serverfiles/mods$ ls
@ace  @advancedrappelling  @advancedslingloading  @advancedtowing  @advancedurbanrappelling  @ares  @cba_a3  @rhsafrf  @rhsusaf
```
The next step will be to adjust the modules line in the top-level `arma3server` script.  The correct `mods=` line in the file that corresponds to the modules presented in the example above would read:
```
mods="mods/@ace\;mods/@advancedrappelling\;mods/@advancedslingloading\;mods/@advancedtowing\;mods/@advancedurbanrappelling\;mods/@ares\;mods/@cba_a3\;mods/@rhsafrf\;mods/@rhsusaf"
```
Note that ONLY the semicolons are escaped.

Start the server and check that your mods all have valid hashes.  You should see something similar to the following in your gameserver log file:
```
arma3server@gamebox3:~$ grep "List of mods" log/console/arma3-server-console.log  -A25
 1:21:05 ============================================================================================= List of mods ===============================================================================================
 1:21:05 modsReadOnly = true
 1:21:05 safeModsActivated = false
 1:21:05 customMods = true
 1:21:05 hash = '24A14A6F1715B508E4C140459CBB736444CA099C'
 1:21:05 hashShort = 'f9bc2cc3'
 1:21:05                                               name |               modDir |    default |               origin |                                     hash | hashShort | fullPath
 1:21:05 ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 1:21:05                          RHS: United States Forces |             @rhsusaf |      false |             GAME DIR | 2f346300316ae1bee109888385a77be1921fc48b |   4c30ccd | /home/arma3server/serverfiles/mods/@rhsusaf
 1:21:05        RHS: Armed Forces of the Russian Federation |             @rhsafrf |      false |             GAME DIR | a9f61612ce09e3eb050dddb477390bbdca8f6f96 |  86f4f4ea | /home/arma3server/serverfiles/mods/@rhsafrf
 1:21:05                       Community Base Addons v3.0.0 |              @cba_a3 |      false |             GAME DIR | 5e4d58da7d3525e9089577880a322b2e9ccf1767 |  dc1227b1 | /home/arma3server/serverfiles/mods/@cba_a3
 1:21:05                                               Ares |                @ares |      false |             GAME DIR | d69f08e52d5102394e3fb5ae0e62fd2cd8409b0c |  e1c60454 | /home/arma3server/serverfiles/mods/@ares
 1:21:05                          Advanced Urban Rappelling | @advancedurbanrappelling |      false |             GAME DIR | f89771ffb164eb32069350428c73bf5ace17fb12 |  7c4278a8 | /home/arma3server/serverfiles/mods/@advancedurbanrappelling
 1:21:05                                    Advanced Towing |      @advancedtowing |      false |             GAME DIR | 3bbdd3d06fbdf74ef0197e92409a34c81edb10d5 |  eb7c2b5d | /home/arma3server/serverfiles/mods/@advancedtowing
 1:21:05                             Advanced Sling Loading | @advancedslingloading |      false |             GAME DIR | 1af4c6ff7f351b09ad5ef4513f3038d44a375117 |  9f2e7c81 | /home/arma3server/serverfiles/mods/@advancedslingloading
 1:21:05                                Advanced Rappelling |  @advancedrappelling |      false |             GAME DIR | 35c56daaba7164fbaadb24b5715caf9216189348 |  7029c1d8 | /home/arma3server/serverfiles/mods/@advancedrappelling
 1:21:05                  Advanced Combat Environment 3.7.0 |                 @ace |      false |             GAME DIR | 1251197941f4565b6fddb807ccc6c88bfbb61113 |  a66ef771 | /home/arma3server/serverfiles/mods/@ace
 1:21:05                                  Arma 3 DLC Bundle |            dlcbundle |       true |            NOT FOUND |                                          |           | 
 1:21:05                                        Arma 3 Apex |            expansion |       true |             GAME DIR | ec40f8295ae63a8b823ae3fb2700b9118ff69072 |  231d7bbe | /home/arma3server/serverfiles/expansion
 1:21:05                                    Arma 3 Marksmen |                 mark |       true |             GAME DIR | a6ae777fb084f739dbdc84cb8a58c864e8fd5ad0 |  f71c9869 | /home/arma3server/serverfiles/mark
 1:21:05                                 Arma 3 Helicopters |                 heli |       true |             GAME DIR | 5b05f65505b7a14ab34754fd014590de8a287023 |  e55c01d5 | /home/arma3server/serverfiles/heli
 1:21:05                                       Arma 3 Karts |                 kart |       true |             GAME DIR | 18cd569ec6fa46f3db80faf3aa51a852874b2028 |  4a0232e1 | /home/arma3server/serverfiles/kart
 1:21:05                                        Arma 3 Zeus |              curator |       true |             GAME DIR | 20a9850c01e340b360399c169fc3bb1cb8bf4dc7 |  ee9ab146 | /home/arma3server/serverfiles/curator
 1:21:05                                             Arma 3 |                   A3 |       true |            NOT FOUND |                                          |           | 
 1:21:05 ==========================================================================================================================================================================================================
```
Good luck.