# Arma 3

## Headless Client

### Headless Client Overview

[https://community.bistudio.com/wiki/Arma\_3\_Headless\_Client](https://community.bistudio.com/wiki/Arma_3_Headless_Client)

* Headless Client is used to offload AI calculations from the server.
* Headless Client is integrated into game client and dedicated server executable \(Windows and Linux, use -client parameter\).
* The server doesn't allow arbitrary connections from headless clients if you do not define the headless clients IPs in the server.cfg.

### Headless Client Setup and Usage

Starting up a headless client and having it connect to your server is easy, Creating a mission that uses the Headless Client is not.

> note: This guide handles the setup and connection ONLY.
>
> note: All references to `arma3server` are referring the script you use to start your server, not the server executable itself unless noted.

1. Create a [new server instance](../features/multiple-game-servers.md) using LinuxGSM `./linuxgsm.sh arma3server`. This will become the headless client instance. Rename the new instance to `arma3server-hc`.

Edit the config file `lgsm/config-lgsm/arma3server-hc.cfg`.

Edit the `port=` increasing the number by a factor of 12 e.g 2303 becomes 2314.

Edit `parms=` changing it to the following.

```text
parms="-client -connect=${ip}:${port} -password=CHANGEME"`
```

Edit the game server config for the ARMA 3 server \(not the headless client\) `arma3server.server.cfg`. Add the headless client IP address to `headlessClients[]=`. If the headless client is on the same physical server as the ARMA 3 server then also add the IP it to `localClient[]=`.

> note: Do not use 127.0.0.1 as the IP address.

`headlessClients[]={"xxx.xxx.xxx.xxx"};    
localClient[]={xxx.xxx.xxx.xxx};` Navigate to your profile directory. By default `cd ~/.local/share/Arma\ 3\ -\ Other\ Profiles` and edit `Player.Arma3Profile` adding the line `battleyeLicense=1;`.

Start your server with `./arma3server start` Start your headless client with `./arma3server-hc start`.

Only a logged in admin can see the headless clients in the player menu on the server. The headless client will connect and automatically assume the first available headless client slot.

## Adding Mods

Incorporating mods into the server is not supported by LinuxGSM. The following guide is a general process for getting modules to load with your server. However, issues loading modules should be taken up with the mod developers.

For a standard deployment, you will want to have your modules unpacked under `serverfiles/mods`. For example, your directory structure might have the following raw modules unpacked under `serverfiles/mods`:

```text
[arma3server@localhost mods]$ ls
@ace @AdvancedTowing @CBA_A3 @RHSUSAF @AdvancedRappelling @AdvancedUrbanRappelling @RHSAFRF @AdvancedSlingLoading @Ares @RHSGREF
```

### Lower Case file names

The server demands that the modules possess all lowercase names. Since not all mods do this all files with uppercase letters will need or be converted. This can be done my using the following script.

Run the script from the `mods` directory.

```bash
#!/bin/bash
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

```text
for ((i=1;i<=${depth};i++))
do
  for x in $(find . -maxdepth $i | grep [A-Z])
  do
    mv $x $(echo $x | tr 'A-Z' 'a-z')
  done
done
```

All mods should now be in lowercase

```text
arma3server@gamebox3:~/serverfiles/mods$ ls
@ace  @advancedrappelling  @advancedslingloading  @advancedtowing  @advancedurbanrappelling  @ares  @cba_a3  @rhsafrf  @rhsusaf
```

Next ensure that all the mods are correctly named in the LinuxGSM config. Ensuring that that only the semicolons are escaped `\`.

```text
mods="mods/@ace\;mods/@advancedrappelling\;mods/@advancedslingloading\;mods/@advancedtowing\;mods/@advancedurbanrappelling\;mods/@ares\;mods/@cba_a3\;mods/@rhsafrf\;mods/@rhsusaf"
```

Start the server and check that your mods all have valid hashes.  
You should see something similar to the following in your gameserver [log](../features/logging.md) file:

```text
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

