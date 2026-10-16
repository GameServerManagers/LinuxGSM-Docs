# SteamCMD

![](<../.gitbook/assets/steamcmd (1).png>)

SteamCMD is a command-line based Steam client developed by Valve that is used to remotely download game files. This is very useful for game servers, as it is significantly easier to keep them up-to-date. Any game that supports dedicated servers will have its server files available on SteamCMD. All you need is the AppID which can be found on Valve's [wiki](https://developer.valvesoftware.com/wiki/Dedicated\_Servers\_List) or [SteamDB](https://steamdb.info/search/?a=app\&q=server).

{% hint style="info" %}
You can only download server files for the operating system that you are using SteamCMD on.
{% endhint %}

![SteamCMD Terminal](../.gitbook/assets/steamcmd.png)

## Network ports

SteamCMD is a downloader. It connects over the Internet to Valve to log in and download or update files. The game server then runs those files and makes its own connections to players and Steam services. The game server can run after SteamCMD exits.

```text
SteamCMD on your machine    --> Valve's login and download services
Game server on your machine --> Valve's Steam services
Players on the Internet    --> Your game server's game/query port
```

The Steam port shown by LinuxGSM belongs to the running game server's communication with Valve. It is not an internal connection between SteamCMD and the game server. In networking documentation, a local port means a port on your machine; it does not mean that the traffic stays on your machine or LAN.

The table below assumes a typical router with stateful NAT and outbound connections allowed. It distinguishes an outbound firewall rule from an inbound port-forwarding rule.

| Activity | Traffic direction | Router port forwarding |
| --- | --- | --- |
| SteamCMD login and downloads | Your machine connects out to Valve | **No.** SteamCMD needs outbound access and reply traffic, not an incoming port-forwarding rule. |
| Public game server: players and queries | Players and server browsers connect in to your machine | **Yes**, for the game's configured incoming ports and protocols. |
| Game server communication with Steam | The game server connects out to Valve | **No** for connections initiated by the server and their replies. Check any additional requirements documented by the particular game. |

For a restrictive outbound firewall, see Valve's [Required Ports for Steam](https://help.steampowered.com/en/faqs/view/2EA8-4D75-DA21-31EB). Its login/download guidance lists TCP 80/443 and TCP/UDP remote ports 27015-27050. Remote ports are the destination ports at Steam, not a range to forward into your game server. Allow reply traffic through a stateful firewall.

Some Source games use a separate local Steam port around 26900/26901. This is not a universal GSLT port or a reason to forward that port for every game. See [Source engine ports](../networking/source-engine.md#steam-backend-port) and the general [ports guide](../networking/ports.md).

## SteamCMD Login

SteamCMD requires a login to download some game servers.

It is recommended that you [create a new Steam username](https://store.steampowered.com/login/) just for the server.

### Anonymous Login

The majority of game servers using SteamCMD only require an _anonymous_ login. LinuxGSM will not require any configuration if this is the case.

### Steam User Login

Some game servers require you to login to SteamCMD using a steam login to allow download of the server. Some also require you to own a copy of the game on the steam account.

If this is the case LinuxGSM will prompt you on installation to set a steam _username_ and _password._ This can be set by editing the following settings within the [LinuxGSM config](../configuration/linuxgsm-config.md).

```
## SteamCMD Login
steamuser="username"
steampass='password'
```

Keep the password in single quotes so characters such as `$` are not expanded.

If you get the error `ERROR! Failed to install app '2430930' (No subscription)` then you do not own a copy of the game in your account and will need to login on the standard steam client and buy the game. If the game is free you will need to "add to account".

Some game servers also need a Steam login for [Workshop downloads](workshop.md#steam-account-requirements), even when the server itself downloads anonymously.

{% hint style="danger" %}
**Do not** use your own steam login. Create a new Steam login just for the game server. The Steam login password is stored in [plain text](#plain-text-passwords).
{% endhint %}

{% hint style="info" %}
Check [here](https://linuxgsm.com/data/steamcmd) for a list of game servers that require a login.
{% endhint %}

### Plain Text Passwords

SteamCMD prints out passwords in plain text meaning that the Steam login password is visible to anyone on the server. LinuxGSM saves logs, and the Steam login password will be viewable in the logs.

## Steam Guard

![Steam Guard](../.gitbook/assets/steamguard.jpg)

Steam Guard is an additional layer of security that can be applied to a Steam account. The first layer is the account login credentials: the Steam account username and password. With Steam Guard, a second layer of security is applied to the account, making it harder for a Steam account to fall into the wrong hands.

If Steam Guard is enabled on an account, a login from an unrecognised device requires an access code as verification. Depending on the account Steam Guard settings, either an email with a code or a code from the Steam Mobile app on a smartphone is required.

{% hint style="info" %}
For more info visit [steam support](https://support.steampowered.com/kb\_article.php?ref=4020-ALZM-5519).
{% endhint %}

### Authentication Methods for SteamCMD

1. Username and password - No Steam Guard
2. Username and password - Steam Guard via Email
3. Username and password - Steam Guard via Smartphone (not compatible with LinuxGSM)

**Username and Password - No Steam Guard**

Simply requires your Steam username and password.

**Username and Password - Steam Guard via Email**

Requires your Steam username and password and you will also receive an email on the first login to SteamCMD and be required to enter a code. Once the code is entered your server is authorised to use the steam account you entered.

**Username and Password - Steam Guard via Smartphone (not compatible with LinuxGSM)**

Requires your Steam Username & Password but also requires you have the Steam app on your phone to use 2-factor Authentication.

### Using Steam Guard with LinuxGSM

Both options 1 & 2 work with LinuxGSM.

Steam Guard via Smartphone is not compatible because it requires a code every time you login to SteamCMD. This is problematic if you want your game servers to auto-update.

If you have Steam Guard via email enabled the first time you start SteamCMD you will be prompted to enter a steam Guard code and you will receive an email with the code. Copy and paste the code into the prompt and press enter. You will not need to enter a code again.
