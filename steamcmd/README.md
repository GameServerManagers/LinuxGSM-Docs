# SteamCMD

## What is SteamCMD?

SteamCMD is a command-line based Steam client developed by Valve that is used to remotely download game files. This is very useful for servers, as this means it's significantly easier to keep them up-to-date, it's also very easy to use. Any game that supports dedicated servers will have their server files available on SteamCMD. All you need is the AppID which can be found on Valve's [wiki](https://developer.valvesoftware.com/wiki/Dedicated_Servers_List) or [SteamDB](https://steamdb.info/search/?a=app&q=server).

> Note: You can only download server files for the Operating System that you are using SteamCMD on.

![SteamCMD Terminal](../.gitbook/assets/steamcmd.png)

## SteamCMD Login

SteamCMD requires a login to use its services.

It is recommended that you [create a new Steam username](https://store.steampowered.com/login/) just for the server.

### Anonymous Login

The majority of game servers through SteamCMD are freely available for download. These servers can be accessed by logging in to SteamCMD as _anonymous_. In this case, Steam variables won't be present in LinuxGSM and you have nothing to worry about.

### Steam User Login

Some game servers require you login to SteamCMD using a steam login to allow download of the server. Some also require you to own a copy of the game on the steam account.

It can be set by by editing the following settings withing your _gameserver_ script.

```text
## SteamCMD Login
steamuser="username"
steampass="password"
```

It is recommended that you create a new Steam username just for the server for security reasons.

For a list of which servers require logins and game purchases visit: [http://linuxgsm.com/list](http://linuxgsm.com/list)

## Plain Text Passwords

SteamCMD prints out passwords in plain text meaning that your Steam password is open for anyone to see on the server. LinuxGSM saves logs and your password will be view-able in the logs.

## Steam Guard

![Steam Guard](../.gitbook/assets/steamguard.jpg)

Steam Guard is an additional level of security that can be applied to your Steam account. The first level of security on your account is your login credentials: your Steam account name and password. With Steam Guard, a second level of security is applied to your account, making it harder for your Steam account to fall into the wrong hands.

When Steam Guard is enabled on your account, when you login to your Steam account from an unrecognized device you'll need to provide a special access code to verify it's your account. Depending on your Steam Guard settings, you'll either receive an email with the special code or you'll get it from the Steam Mobile app on your smartphone.

For more info visit: [https://support.steampowered.com/kb\_article.php?ref=4020-ALZM-5519](https://support.steampowered.com/kb_article.php?ref=4020-ALZM-5519)

### Authentication Methods for SteamCMD

1. Username and Password - No Steam Guard
2. Username & Password - Steam Guard via Email \(recommended\)
3. Username & Password - Steam Guard via Smartphone \(not compatible with LinuxGSM\)

#### Username & Password - No Steam Guard

Simply requires your Steam Username and Password.

#### Username & Password - Steam Guard via Email \(recommended\)

Requires your Steam Username & Password but also you will receive and email on first login to SteamCMD and be required to enter a code. Once the code is entered your server is authorized to use the steam account you entered.

#### Username & Password - Steam Guard via Smartphone \(not compatible with LinuxGSM\)

Requires your Steam Username & Password but also requires you have the Steam app on your phone to use 2-factor Authentication

### Using Steam Guard with LinuxGSM

Both options 1 & 2 work with LinuxGSM. You can either have Steam Guard disabled or have Steam Guard via email.

Steam Guard via Smartphone is not compatible because it requires a code every time you login to SteamCMD. This is problematic if you want your servers to auto update.

If you have Steam Guard via email enabled the first time you start SteamCMD you will be prompt to enter a steam Guard code and receive an email with the code. Copy & Paste the code in to the prompt and press enter. You will not need to enter a code again.

## Errors

If you encounter an error like

`Error! App '<app_number>' state is 0x202 after update job.`

there is a good chance that you have run out of disk space.

# Game Server Login Token (GSLT)

**Game Server Login Token is a new system by Valve for managing Game servers.**

> Note: Every single server must use a unique GSLT.

## Games using GSLT

* Ballistic Overkill
* Brainbread 2
* Black Mesa: Deathmatch
* Counter Strike: Global Offensive \(**required**\)
* Counter Strike: Source \(**required**\)
* Day of Defeat: Source
* Empires Mod
* Garry’s Mod
* Insurgency
* No more Room in Hell \(**required**\)
* Team Fortress 2
* Tower Unite
* Zombie Panic! Source

## Generate a token

> Use the app ID of the base game \(e.g. 440 for TF2, 730 for CS:GO, 4000 for Garry's Mod\) when generating a token

To generate a token follow this link. You will be required to login to a steam account. I recommend a separate account from your main steam account. [http://steamcommunity.com/dev/managegameservers](http://steamcommunity.com/dev/managegameservers)

## New command line Parameter

GSLTs can be registered on your server\(s\) by using the _sv\_setsteamaccount_ command either in _autoexec.cfg_ or from a start parameter.

on the server startup line.

`+sv_setsteamaccount [token]`

autoexec.cfg

`sv_setsteamaccount [token]`

## Tower Unite

Tower Unite has a command within its config file

`SteamLoginToken=`

## What is the point of GSLT?

To fully understand the reasoning behind GSLTs, we need to back up a bit to July 2015. [Valve announced that running certain plugins would get your server blacklisted](http://dathost.net/blog/important-information-regarding-our-csgo-servers/), meaning it could not connect to the master servers and people wouldn’t be able to connect to the server.

This created a lot of problems for gameserver providers, large communities and anyone providing configurable servers to third parties, as bans were handed out by IP, meaning that an entire machine could be banned because of one malicious or uninformed user.

To address this, Valve is moving the ban to account-level instead of IP-level, which means that the end-user is always responsible for what they run on their server. Of course, gameserver providers and the like still have a responsibility to educate their users on these policies, as some might mistakenly upload blacklisted plugins.

An added benefit is that people who add your server to favorites will still be able to find and connect to your server, even if you change hosting provider and/or the IP / port of your server. This was something that previously was impossible.

## Advantages of using GSLT

GSLT creates a persistent token for your game server. This allows any users who have favorited your server to still find your server if you to change your servers IP details. This is very useful if you change your server/hosting provider. Allowing your regular players to easily connect to your new server.

## FAQ

### If one of my tokens are banned/blacklisted, will all tokens be banned?

Yes, all of the tokens on your account will be blacklisted if one of your servers \(tokens\) is found to be running a blacklisted plugin. Make sure you read up on Valve’s plugin policies before running your servers so nothing unfortunate happens to your tokens.

### If my GSLTs get banned for running a blacklisted plugin, will my steam account be community and/or VAC banned?

Depending on the game Valve will punish the account that generated the token, On CS:GO you get a global cooldown of 7 days \(you cannot join any community/valve server\) Most likely, it won’t be VAC banned, but Valve’s requirement that anyone creating GSLTs is not community banned, you may be community banned for running blacklisted plugins.

### Can I use the same GSLT for multiple servers?

No. You must create a unique GSLT for each simultaneously running server.

### Can I re-use GSLTs?

Yes, you can add your GSLT to a new server, you just can’t run two servers with the same GSLT, at the same time.

### Do I still need a Steam WebAPI key to host workshop maps?

Unfortunately, despite registering a GSLT to your server, CS:GO servers will still need a Steam WebAPI key to host maps from the Workshop.

### Will this also affect Team Fortress 2?

As of yet, no official confirmation has been made that TF2 servers will also require GSLTs, but they do support them so it’s not a wild guess that this is to come.

### My server loses connection to the registered Steam account

Don’t use the same GSLT for multiple servers. When a server starts with a specific GSLT, it will disconnect any other servers already running that same GSLT. You need to create a unique GSLT for each server.

### Is there a limit on how many GSLTs my account can have?

Yes, you can have a maximum of 1000 GSLTs on your account.

### What are the requirements for my account to be able to create a GSLT?

Your Steam account must not be currently community banned or locked. Your Steam account must not be limited. Your Steam account must have a qualifying registered phone. Your Steam account must own the game for which you are creating a GSLT. Your Steam account may not have more than 1000 tokens.

### Can I run servers without GSLTs?

Yes CS:GO is the only internet connected server that requires GSLT currently.

For further information see this useful blog post: [http://dathost.net/blog/important-information-regarding-our-csgo-servers/](http://dathost.net/blog/important-information-regarding-our-csgo-servers/)



