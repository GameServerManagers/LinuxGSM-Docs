# Discord

![](../.gitbook/assets/discord_logo-1.png)

## Create a Discord Webhook

A webhook is required to post alerts to a Discord text channel

1. Right-click on the text channel you want to use and select `edit channel`.
2. Select `Webhooks` &gt; `Create Webhook`
3. Name: LinuxGSM
4. Icon:
5. Copy the Webhook URL
6. Turn on discord alert and enter the URL in to the LinuxGSM settings. \(`~/lgsm/config-lgsm/<gameserver>/common.cfg`\)

```text
# Discord Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Discord
discordalert="on"
discordwebhook="https://discordapp.com/api/webhooks/3539332633367897009/5t_K4GkuBaR2-69TsKqXmHIya1ck1tirnu_Fst-DUC00dye98eaa_I6uTIcHEsi7a17K"
```

{% hint style="info" %}
You must have Discord _User Settings &gt; Text & Images &gt; Link Preview: 'Show website preview...'_ enabled or you will just see blank messages from the alert bot.
{% endhint %}

