# Killing Floor 2

## Ports

**Game Port** Default: 7777 UDP Handled by: `LinuxServer-KFEngine.ini` **Query Port** Default: 27015 UDP Handled automatically or handled by parameters. Formula for finding query port assigned automatically is 19238 + assigned game port. **Web Admin** Default: 8080 TCP Handled by: `KFWeb.ini` **Steam Port** Default: 20560 UDP Handled automatically. Formula for finding steam port is 12783 + assigned game port.

## Resources

[Killing Floor 2 Official Server Wiki](https://wiki.tripwireinteractive.com/index.php?title=Dedicated_Server_%28Killing_Floor_2%29)

## Killing Floor 2 Config Files- Note- Will not merge until finished

Killing floor 2 generates config files on first startup, these will be located inside /KFGame/config/kf2server/ and are the config files that take priority. Relevent Config Files:

LinuxServer-KFEngine.ini

\`\`

**LinuxServer-KFGame.ini**

Game Settings

GameDifficulty=

GameLength=

_MOTD Settings- This can also be edited using the server's web interface_

BannerLink=http://website/image.png 

ServerMOTD=Server join message

WebsiteLink=[http://w](http://www.camarillagaming.com)ww.link\_to\_website.com

ClanMotto=Bottom text in MOTD

Server Name

ServerName=Full name that shows up in server browser

ShortName=Short name



**KFWeb.ini**

`ListenPort="port"`

Determines port server listens on for web interface.

`bEnabled=true or false`

Turns web interface on and off



Config files guide-&gt;Using web interface guide-&gt;Setting up steam workshop guide



