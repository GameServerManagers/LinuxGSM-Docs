# Workshop

Many Steam games support the steam [workshop](https://steamcommunity.com/workshop). It is an easy way to share community maps and addons and is very useful for custom servers, without needing to worry about setting up [FastDL](../commands/fastdl.md). LinuxGSM adds workshop pre-configuration to game server scripts as when available.

You will need a Steam API key, a collection to subscribe to \(you can create one\), and some config parameters in your [LinuxGSM config](../configuration/linuxgsm-config.md).

## Getting a Steam API Key

Simply go to [https://steamcommunity.com/dev/apikey](https://steamcommunity.com/dev/apikey) and follow instructions.

{% hint style="danger" %}
Do not share this key.
{% endhint %}

## Creating a collection and get the collection ID

Go browse collections for your desired game, and click "Create a collection".

* CS:GO : [https://steamcommunity.com/workshop/browse/?section=collections&appid=730](https://steamcommunity.com/workshop/browse/?section=collections&appid=730)
* Garry's Mod : [https://steamcommunity.com/workshop/browse/?section=collections&appid=4000](https://steamcommunity.com/workshop/browse/?section=collections&appid=4000)

Add some addons to the collection, then publish the completed collection. Then get the collection page id which can be found on the page URL. For example:

```text
https://steamcommunity.com/sharedfiles/filedetails/?id=274397080
```

The collection id would be `274397080`.

## Server Configurations

### Garry's Mod

For Garry's Mod, edit these lines in your [LinuxGSM config](../configuration/linuxgsm-config.md)

```text
wsapikey="YOUR_STEAM_API_KEY"
wscollectionid="YOUR_COLLECTION_ID"
```

Setting the workshop collection ID only adds content to the server, and players will only download maps from the collection. This is because workshop files must be set in the workshop.lua file in:

`/home/gmod/serverfiles/garrysmod/lua/autorun/server/`

Example line:

```text
resource.AddWorkshop( "workshop_ID_#_here" ) --comment
resource.AddWorkshop( "1728099077" ) --Rick Roll SENT
```

I do not recommend putting a collection ID in this file if you are hosting a server with a large map list, this will cause players to download every map on their first connection. Instead it is recommended to put every individual workshop item except maps in this file.

### Counter-Strike Global Offensive

For CSGO, edit these lines in your [LinuxGSM config](../configuration/linuxgsm-config.md)

```text
wsapikey="YOUR_STEAM_API_KEY"
wscollectionid="YOUR_COLLECTION_ID"
wsstartmap="
```

### **Killing Floor 2**

For KF2 Server using LinuxGSM, workshop content is added in `LinuxServer-KFEngine.ini` under:

/home/user/serverfiles/KFGame/Config/kf2server

[Official Guide Here](https://wiki.killingfloor2.com/index.php?title=Dedicated_Server_%28Killing_Floor_2%29#Setting_Up_Steam_Workshop_For_Servers)

While following the guide, remember `PCServer-KFEngine.ini` is instead `LinuxServer-KFEngine.ini`

[Killing floor 2 has a known workshop problem.](../game-servers/killing-floor-2.md)



