# SteamCMD

![](../.gitbook/assets/steamcmd%20%281%29.png)

SteamCMD is a command-line based Steam client developed by Valve that is used to remotely download game files. This is very useful for game servers, as it is significantly easier to keep them up-to-date. Any game that supports dedicated servers will have its server files available on SteamCMD. All you need is the AppID which can be found on Valve's [wiki](https://developer.valvesoftware.com/wiki/Dedicated_Servers_List) or [SteamDB](https://steamdb.info/search/?a=app&q=server).

{% hint style="info" %}
You can only download server files for the operating system that you are using SteamCMD on.
{% endhint %}

![SteamCMD Terminal](../.gitbook/assets/steamcmd.png)

## SteamCMD Login

SteamCMD requires a login to download some game servers.

It is recommended that you [create a new Steam username](https://store.steampowered.com/login/) just for the server.

### Anonymous Login

The majority of game servers using SteamCMD only require an _anonymous_ login. LinuxGSM will not require any configuration if this is the case.

### Steam User Login

Some game servers require you to login to SteamCMD using a steam login to allow download of the server. Some also require you to own a copy of the game on the steam account.

If this is the case LinuxGSM will prompt you on install to set a steam _username_ and _password._ This can be set by editing the following settings within the [LinuxGSM config](../configuration/linuxgsm-config.md).

```text
## SteamCMD Login
steamuser="username"
steampass="password"
```

{% hint style="danger" %}
**Do not** use your own steam login. Create a new Steam login just for the game server. As the steam login password is stored in [plain text](./#plain-text-passwords).
{% endhint %}

{% hint style="info" %}
Check [here](https://linuxgsm.com/data/steamcmd) for a list of game servers that require a login.
{% endhint %}

### Plain Text Passwords

SteamCMD prints out passwords in plain text meaning that the Steam login password is visible to anyone on the server. LinuxGSM saves logs and the Steam login password will be view-able in the logs.

## Steam Guard

![Steam Guard](../.gitbook/assets/steamguard.jpg)

Steam Guard is an additional layer of security that can be applied to a Steam account. The first layer is the account login credentials: the Steam account username and password. With Steam Guard, a second layer of security is applied to the account, making it harder for a Steam account to fall into the wrong hands.

If Steam Guard is enabled on an account when a login to from an unrecognized device happens an access code will be required as verification. Depending on the account Steam Guard settings, either an email with a code or a code from the Steam Mobile app on a smartphone is required.

{% hint style="info" %}
For more info visit [steam support](https://support.steampowered.com/kb_article.php?ref=4020-ALZM-5519).
{% endhint %}

### Authentication Methods for SteamCMD

1. Username and password - No Steam Guard
2. Username and password - Steam Guard via Email
3. Username and password - Steam Guard via Smartphone \(not compatible with LinuxGSM\)

**Username and Password - No Steam Guard**

Simply requires your Steam username and password.

**Username and Password - Steam Guard via Email**

Requires your Steam username and password and you will also receive an email on the first login to SteamCMD and be required to enter a code. Once the code is entered your server is authorised to use the steam account you entered.

**Username and Password - Steam Guard via Smartphone \(not compatible with LinuxGSM\)**

Requires your Steam Username & Password but also requires you have the Steam app on your phone to use 2-factor Authentication.

### Using Steam Guard with LinuxGSM

Both options 1 & 2 work with LinuxGSM.

Steam Guard via Smartphone is not compatible because it requires a code every time you login to SteamCMD. This is problematic if you want your game servers to auto-update.

If you have Steam Guard via email enabled the first time you start SteamCMD you will be prompted to enter a steam Guard code and you will receive an email with the code. Copy and paste the code into the prompt and press enter. You will not need to enter a code again.

## 

