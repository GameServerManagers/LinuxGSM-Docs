<a href="https://discordapp.com"><p align="center"><img src="images/discord/discord_logo.png" alt="Discord logo" /></a>

<p align="center">Send LinuxGSM alerts to a Discord server.</p>

# Create a Discord Webhook
A webhook is required to post alerts to a Discord text channel

1. Right-click on the text channel you want to use and select `edit channel`.

2. Select `Webhooks` > `Create Webhook`
* Name: LinuxGSM
* Icon:

3. Copy the Webhook URL

4. Turn on discord alert and enter the URL in to the LinuxGSM settings.
```
# Discord Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Discord
discordalert="on"
discordwebhook="https://discordapp.com/api/webhooks/3539332633367897009/5t_K4GkuBaR2-69TsKqXmHIya1ck1tirnu_Fst-DUC00dye98eaa_I6uTIcHEsi7a17K"
```

_Note: You must have Discord User Settings > Text & Images > Link Preview: 'Show website preview...' enabled or you will just see blank messages from the alert bot._