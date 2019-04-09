# gamedig

[Gamedig](https://github.com/sonicsnes/node-gamedig) is a tool that queries game servers and returns outputs data from a query in to json format. It can return not only if the game server is online but various data such as current maps and players. This allows `./gameserver details` to display live information.

Gamedig super-seeds gsquery as the tool to monitor game servers. gamedig is currently optional and gsquery is kept to ensure compatibility because of gamedig requiring nodejs to be installed.

## Install Gamedig

Gamedig must have nodejs installed to work. Run the following command to install nodejs.

### Remove existing NodeJS

You might already have an older version of nodejs installed or be having issues with node dependencies. Try fully removing nodejs first then following the instructions below to install.

```text
sudo apt remove --purge nodejs npm
sudo apt clean
sudo apt autoclean
sudo apt install -f
sudo apt autoremove
```

### Install NodeJS

Installing nodejs can be problematic, however using the below should work well.

#### Ubuntu/Debian

```text
sudo apt install curl
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install -y nodejs
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
sudo apt update && sudo apt install yarn
```

#### CentOS

{% hint style="danger" %}
Work in progress
{% endhint %}

#### Fedora

{% hint style="danger" %}
Work in progress
{% endhint %}

### Install Gamedig npm

Once nodejs is installed use npm to install gamedig using the following command.

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

