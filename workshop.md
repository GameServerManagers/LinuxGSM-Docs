# Workshop

Many Steam games now support the workshop. It's an easy way to share updated maps or addons between client and servers, without worrying about setting up any kind of FastDL. LinuxGSM adds workshop pre-configuration to game server scripts as soon as possible.

You will have to get a Steam API, a collection to subscribe to \(you can create one\), and ultimately, edit two or three configuration variables \(start parameters\) in your LinuxGSM config.

## Getting a Steam API Key

Simply go to [https://steamcommunity.com/dev/apikey](https://steamcommunity.com/dev/apikey) and follow instructions.

Try not to share this key.

## Creating a collection and get the collection ID

Go browse collections for your desired game, and click "Create a collection".

For CS GO : [https://steamcommunity.com/workshop/browse/?section=collections&appid=730](https://steamcommunity.com/workshop/browse/?section=collections&appid=730)

For Garry's Mod : [https://steamcommunity.com/workshop/browse/?section=collections&appid=4000](https://steamcommunity.com/workshop/browse/?section=collections&appid=4000)

Add some addons to it, then publish it. It won't work if you don't publish the collection. Then, while being in your collection page, get the digits at the end of the URL : This is your collection ID.

## Configuration Variables

Simply edit your \[\[LinuxGSM Config\]\]

### Garry's Mod

For Garry's Mod, edit those 2 lines accordingly in your \[\[LinuxGSM Config\]\]:

`workshopauth="YOUR_STEAM_API_KEY"`

`workshopcollectionid="YOUR_COLLECTION_ID"`

### Counter-Strike Global Offensive

For CSGO, have a look at these lines in your in your \[\[LinuxGSM Config\]\]:

```text
# authkey=""
# ws_collection_id=""
# ws_start_map=""
```

Remove the hashtags, then add your values.

