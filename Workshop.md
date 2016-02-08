# Workshop support

Many Steam games now support the workshop. It's an easy way to share updated maps or addons between client and servers, without worrying about setting up any kind of FastDL. LGSM adds workshop pre-configuration to game server script as soon as possible.

You will have to get a Steam API, a collection to subscribe to (you can create one), and ultimately, edit a bunch a configuration variables in your main script.

## Configuration Variables

Simply edit your script accordingly

### Garry's Mod

For Garry's Mod, edit those 2 lines accordingly in your "gmodserver" script.

`workshopauth="YOUR_STEAM_API_KEY"`

`workshopcollectionid="YOUR_COLLECTION_ID"`

### Counter-Strike Global Offensive

For CSGO, have a look at these lines in your "csgoserver" file :

`# authkey=""`

`# ws_collection_id=""`

`# ws_start_map=""`

(https://github.com/dgibbs64/linuxgsm/blob/master/CounterStrikeGlobalOffensive/csgoserver#L53-L55)

Remove the hashtags, then add your values. 


## Getting a Steam API Key

Simply go to https://steamcommunity.com/dev/apikey and follow instructions.

Try not to share this key.

## Creating a collection and get the collection ID

Go browse collections for your desired game, and click "Create a collection".

For CS GO : https://steamcommunity.com/workshop/browse/?section=collections&appid=730

For Garry's Mod : https://steamcommunity.com/workshop/browse/?section=collections&appid=4000

Add some addons to it, then publish it (very important !). Then, while being in your collection page, get the digits at the end of the URL : This is your collection ID. 