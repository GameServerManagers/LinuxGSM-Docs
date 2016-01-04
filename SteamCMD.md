# What is SteamCMD?

SteamCMD is a command-line based Steam client developed by Valve that is used to remotely download game files.
This is very useful for servers, as this means it's significantly easier to keep them up-to-date, It's also very easy to use. Any game that supports dedicated servers will have their server files available on SteamCMD. All you need is the AppID which can be found on Valve's [wiki](https://developer.valvesoftware.com/wiki/Dedicated_Servers_List) or [SteamDB](https://steamdb.info/search/?a=app&q=server).

**Note:** You can only download server files for the Operating System that you are using SteamCMD on.

# SteamCMD Login?
SteamCMD requires a login to use its services.

It is recommended that you [create a new Steam username](https://store.steampowered.com/login/) just for the server.

## Anonymous Login

The majority of game servers through SteamCMD are freely available to download. These servers can be accessed by logging in to SteamCMD as _anonymous_.

## Steam User Login

Some game servers require you login to SteamCMD using a steam login to allow download of the server. Some also require you to own a copy of the game on the steam accout.

It is recommended that you create a new Steam username just for the server for security reasons.

For a list of which servers require logins and game purchases visit: http://gameservermanagers.com/list
# Plain Text Passwords
SteamCMD prints out passwords in plain text meaning that your Steam password is open for anyone to see on the server. LGSM saves logs and your password will be viewable on the logs.

# Steam Guard
Steam Guard is an additional level of security that can be applied to your Steam account. The first level of security on your account is your login credentials: your Steam account name and password. With Steam Guard, a second level of security is applied to your account, making it harder for your Steam account to fall into the wrong hands.

When Steam Guard is enabled on your account, when you login to your Steam account from an unrecognized device you'll need to provide a special access code to verify it's your account. Depending on your Steam Guard settings, you'll either receive an email with the special code or you'll get it from the Steam Mobile app on your smartphone.

For more info visit: https://support.steampowered.com/kb_article.php?ref=4020-ALZM-5519

## Authentication Methods for SteamCMD

1. Username and Password - No Steam Guard
2. Username & Password - Steam Guard via Email (recommended)
3. Username & Password - Steam Guard via Smartphone (not compatible with LGSM)

### Username & Password - No Steam Guard

Simply requires your Steam Username and Password.

### Username & Password - Steam Guard via Email (recommended)

Requires your Steam Username & Password but also you will receive and email on first login to SteamCMD and be required to enter a code. Once the code is entered your server is authorized to use the steam account you entered.

### Username & Password - Steam Guard via Smartphone (not compatible with LGSM)

Requires your Steam Username & Password but also requires you have the Steam app on your phone to use 2-factor Authentication

## Using Steam Guard with LGSM

Both options 1 & 2 work with LGSM. You can either have Steam Guard disabled or have Steam Guard via email.

Steam Guard via Smartphone is not compatible because it requires a code every time you login to SteamCMD. This is problematic if you want your servers to auto update.

If you have Steam Guard via email enabled the first time you start SteamCMD you will be prompt to enter a steam Guard code and receive an email with the code. Copy & Paste the code in to the prompt and press enter. You will not need to enter a code again.