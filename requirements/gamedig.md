# gamedig

[GameDig](https://github.com/gamedig/node-gamedig) is a tool that queries game servers and returns outputs data from a query into json format. It can not only check if the game server is online but also return various data such as current maps and players. This allows `./gameserver details` to display live information.

GameDig super-seeds gsquery as the tool to monitor game servers. GameDig is currently optional but recommended and gsquery is kept to ensure compatibility as gamedig requires Node.js to be installed.

## Install Node.js

GameDig requires [Node.js](https://nodejs.org) a JavaScript runtime environment installed to work. Use the following instructions to install Node.js.

### Remove existing NodeJS

If you already have an older version of nodejs installed or be having issues with node dependencies. It may be worth reinstalling Node.js.

#### Ubuntu/Debian

```bash
sudo apt remove --purge nodejs npm
sudo apt clean
sudo apt autoclean
sudo apt install -f
sudo apt autoremove
```

#### CentOS

{% hint style="warning" %}
Work in progress
{% endhint %}

### Install NodeJS

Installing nodejs can be problematic, however, using the below should work well.

#### Ubuntu/Debian

{% embed url="https://github.com/nodesource/distributions#ubuntu-versions" %}

{% embed url="https://github.com/nodesource/distributions#debian-versions" %}

#### Enterprise Linux Based Distributions

{% embed url="https://github.com/nodesource/distributions#enterprise-linux-based-distributions" %}

### Install GameDig npm

Once nodejs is installed use npm to install gamedig with the following command.

```bash
npm install gamedig -g
```

## Update GameDig

Updates to GameDig are regularly made. It is possible to update by running the npm update command.

```bash
npm update -g
```

You can also see which version of gamedig is installed by running the following.

```bash
 npm list -g gamedig
```

## Sample output

### Details

Extra info becomes available for game server details.

```text
Players:          0/8
Current Map:      Outpost
```

## Raw output

```bash
gamedig --type "protocol-valve" --host "1.2.3.4" --port "27015"
```

```json
{
	"name": "LinuxGSM Server",
	"map": "StationKappa",
	"password": false,
	"raw": {
		"protocol": 17,
		"folder": "StickyBots",
		"game": "StickyBots",
		"steamappid": 0,
		"numplayers": 0,
		"numbots": 0,
		"listentype": "d",
		"environment": "l",
		"secure": 0,
		"version": "0.0.6.22",
		"port": 7777,
		"steamid": "90122418420694019",
		"tags": "BUILDID:622,OWNINGID:90122418420694019,OWNINGNAME:LinuxGSM Server,P2PADDR:90122418420694019,P2PPORT:7777,SESSIONFLAGS:171",
		"gameid": "889400",
		"rules": {
			"BUILDID_i": "622",
			"NP_i": "0",
			"OWNINGID": "90122418420694019",
			"OWNINGNAME": "LinuxGSM Server",
			"P2PADDR": "90122418420694019",
			"P2PPORT": "7777",
			"SESSIONFLAGS": "171",
			"SN_s": "LinuxGSM Server"
		}
	},
	"maxplayers": 8,
	"players": [],
	"bots": [],
	"query": {
		"host": "1.2.3.4",
		"address": "1.2.3.4",
		"port": 27015,
		"port_query": 27015,
		"type": "protocol-valve",
		"duration": 90,
		"attempts": 1
	}
}
```
