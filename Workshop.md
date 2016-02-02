# Workshop support

Many Steam games now support the workshop. It's an easy way to share updated maps or addons between client and servers, without worrying about setting up any kind of FastDL. LGSM adds workshop pre-configuration to game server script as soon as possible.

Simply edit those variables accordingly in your main script

`workshopauth="YOUR_STEAM_API_KEY"`

`workshopcollectionid="YOUR_COLLECTION_ID"`

## Getting a Steam API Key

Simply go to https://steamcommunity.com/dev/apikey and follow instructions.

Try not to share this key.

## Creating a collection and get the collection ID

Go browse collections for your desired game, and click "Create a collection".
Add some addons to it, then publish it (very important !). Then, while being in your collection page, get the digits at the end of the URL : This is your collection ID. 