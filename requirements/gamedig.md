# gamedig

[GameDig](https://github.com/sonicsnes/node-gamedig) is a tool that queries game servers and returns outputs data from a query in to json format. It can return not only if the game server is online but various data such as current maps and players. This allows `./gameserver details` to display live information.

GameDig super-seeds gsquery as the tool to monitor game servers. gamedig is currently optional and gsquery is kept to ensure compatibility because of gamedig requiring Node.js to be installed.

## Install Node.js

GameDig requires [Node.js](https://nodejs.org) a JavaScript runtime environment installed to work. Use the following instuctions to install Node.js.

### Remove existing NodeJS

If you already have an older version of nodejs installed or be having issues with node dependencies. It may be worth reinstalling Node.js.

#### Ubuntu/Debian

```text
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

Installing nodejs can be problematic, however using the below should work well.

#### Ubuntu/Debian

```text
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
sudo apt update && sudo apt install -y nodejs yarn
```

#### CentOS

```text
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo -o /etc/yum.repos.d/yarn.repo
yum install nodejs
yum install yarn
```

### Install GameDig npm

Once nodejs is installed use npm to install gamedig with the following command.

```text
npm install gamedig -g
```

## Sample output

### Details

Extra info becomes available for game server details.

```text
Players:          0/8
Current Map:      Outpost
```

## Raw output

```text
gamedig --type "protocol-valve" --host "1.2.3.4" --port "27015"
```

```text
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

