# Workshop

Many Steam games support the steam [workshop](https://steamcommunity.com/workshop). It is an easy way to share community maps and addons and is very useful for custom servers, without needing to worry about setting up [FastDL](../commands/fastdl.md). LinuxGSM adds workshop pre-configuration to game server scripts as when available.

You will need a Steam API key, a collection to subscribe to \(you can create one\), and some config parameters in your LinuxGSM config.

## Getting a Steam API Key

Simply go to [https://steamcommunity.com/dev/apikey](https://steamcommunity.com/dev/apikey) and follow instructions.

{% hint style="danger" %}
Don't share this key.
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

## Configuration Variables

Edit the [LinuxGSM config](../configuration/linuxgsm-config.md).

### Garry's Mod

For Garry's Mod, edit those 2 lines accordingly in your [LinuxGSM config](../configuration/linuxgsm-config.md)

```text
wsapikey="YOUR_STEAM_API_KEY"
wscollectionid="YOUR_COLLECTION_ID"
```

### Counter-Strike Global Offensive

For CSGO, have a look at these lines in your in your [LinuxGSM config](../configuration/linuxgsm-config.md)

```text
wsapikey="YOUR_STEAM_API_KEY"
wscollectionid="YOUR_COLLECTION_ID"
wsstartmap="
```
