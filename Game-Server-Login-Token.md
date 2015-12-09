**Game Server Login Token is a new system by Valve for managing Game servers.**

_A token is now required for running public CS:GO servers and TF2 is optional._

# Generate a token
To generate a token follow this link. You will be required to login to a steam account. I recommend a separate account from your main steam account
.
[http://steamcommunity.com/dev/managegameservers](http://steamcommunity.com/dev/managegameservers)

# What is the point of GSLT?
To fully understand the reasoning behind GSLTs, we need to back up a bit to July 2015. [Valve announced that running certain plugins would get your server blacklisted](http://dathost.net/blog/important-information-regarding-our-csgo-servers/), meaning it could not connect to the master servers and people wouldn’t be able to connect to the server.

This created a lot of problems for gameserver providers, large communities and anyone providing configurable servers to third parties, as bans were handed out by IP, meaning that an entire machine could be banned because of one malicious or uninformed user.

To address this, Valve is moving the ban to account-level instead of IP-level, which means that the end-user is always responsible for what they run on their server. Of course, gameserver providers and the like still have a responsibility to educate their users on these policies, as some might mistakenly upload blacklisted plugins.

An added benefit is that people who add your server to favorites will still be able to find and connect to your server, even if you change hosting provider and/or the IP / port of your server. This was something that previously was impossible.

# Advantages of using GSLT
GSLT creates a persistent token for your game server. This allows any users who have favorited your server to still find your server if you to change your servers IP details. This is very useful if you change your server/hosting provider. Allowing your regular players to easily connect to your new server.

# Currently Supported Servers
* Counter-Strike: Global Offensive 
* Team Fortress 2 (GSLT not yet required for public servers)

# FAQ

## If one of my tokens are banned/blacklisted, will all tokens be banned?
Yes, all of the tokens on your account will be blacklisted if one of your servers (tokens) is found to be running a blacklisted plugin. Make sure you read up on Valve’s plugin policies before running your servers so nothing unfortunate happens to your tokens.

## If my GSLTs get banned for running a blacklisted plugin, will my steam account be community and/or VAC banned?
No one knows just yet what will happen to the steam account itself. Most likely, it won’t be VAC banned, but Valve’s requirement that anyone creating GSLTs is not community banned, you may be community banned for running blacklisted plugins.

## Can I use the same GSLT for multiple servers?
No. You must create a unique GSLT for each simultaneously running server.

## Can I re-use GSLTs?
Yes, you can add your GSLT to a new server, you just can’t run two servers with the same GSLT, at the same time.

## Do I still need a Steam WebAPI key to host workshop maps?
Unfortunately, despite registering a GSLT to your server, CS:GO servers will still need a Steam WebAPI key to host maps from the Workshop.

## Will this also affect Team Fortress 2?
As of yet, no official confirmation has been made that TF2 servers will also require GSLTs, but they do support them so it’s not a wild guess that this is to come.

## My server loses connection to the registered Steam account
Don’t use the same GSLT for multiple servers. When a server starts with a specific GSLT, it will disconnect any other servers already running that same GSLT. You need to create a unique GSLT for each server.

## Is there a limit on how many GSLTs my account can have?
Yes, you can have a maximum of 1000 GSLTs on your account.

## What are the requirements for my account to be able to create a GSLT?
Your Steam account must not be currently community banned or locked.
Your Steam account must not be limited.
Your Steam account must have a qualifying registered phone.
Your Steam account must own the game for which you are creating a GSLT.
Your Steam account may not have more than 1000 tokens.

## Can I run servers without GSLTs?
No, you need to have a GSLT to run your CS:GO server.

For further information see this useful blog post: [http://dathost.net/blog/important-information-regarding-our-csgo-servers/](http://dathost.net/blog/important-information-regarding-our-csgo-servers/)