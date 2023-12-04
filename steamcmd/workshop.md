# Workshop

Many Steam games support the Steam [workshop](https://steamcommunity.com/workshop). It is an easy way to share community maps and is very useful for custom servers, without needing to worry about setting up [FastDL](../commands/fastdl.md). LinuxGSM adds workshop pre-configuration to game server scripts when available.

You will need a Steam API key, a collection to subscribe to (you can create one), and some config parameters in your [LinuxGSM config](../configuration/linuxgsm-config.md).

## Supported Games Servers

This is a list of game servers that are known to support Workshop

* Ark: Survival Evolved
* ARMA 3
* Day of Infamy
* Counter-Strike 2
* Garrys Mod
* Hurtworld
* Insurgency: Sandstorm
* Killing Floor 2
* Natural Selection 2
* Starbound

## Getting a Steam API/AUTH Key

{% hint style="danger" %}
Do not share this key.
{% endhint %}

Go to [https://steamcommunity.com/dev/apikey](https://steamcommunity.com/dev/apikey) and follow the instructions to get an API/AUTH key.

## Create a Collection and get the Collection ID

{% hint style="info" %}
It is possible to use an existing collection or create your own
{% endhint %}

Go browse collections for your desired game, and click "Create a Collection".

* Counter-Strike 2: [https://steamcommunity.com/workshop/browse/?section=collections\&appid=730](https://steamcommunity.com/workshop/browse/?section=collections\&appid=730)
* Garry's Mod: [https://steamcommunity.com/workshop/browse/?section=collections\&appid=4000](https://steamcommunity.com/workshop/browse/?section=collections\&appid=4000)

Add any maps to the collection, then publish the completed collection. Then get the collection ID which can be found on the page URL. The collection id would be `157384458`.

```
https://steamcommunity.com/sharedfiles/filedetails/?id=157384458
```

## Server Configurations

### **Killing Floor 2**

For KF2 Server using LinuxGSM, workshop content is added in `LinuxServer-KFEngine.ini` under:

/home/user/serverfiles/KFGame/Config/kf2server

[Official Guide Here](https://wiki.killingfloor2.com/index.php?title=Dedicated\_Server\_\(Killing\_Floor\_2\)#Setting\_Up\_Steam\_Workshop\_For\_Servers)

While following the guide, remember `PCServer-KFEngine.ini` is instead `LinuxServer-KFEngine.ini`

[Killing Floor 2 has a known workshop problem.](../game-servers/killing-floor-2.md)
