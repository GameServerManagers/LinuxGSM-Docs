# Discord

![](<../.gitbook/assets/discord\_logo (1).png>)

[Discord](https://discordapp.com) is a VoIP app that allows other applications to send messages via a webhook. This functionality is used to allow users to recieve alerts about LinuxGSM.

## Create a Discord Webhook

A webhook is required to post alerts to a Discord text channel

1. Right-click on the text channel you want to use and select `Edit channel`.
2. Select `Webhooks` > `Create Webhook`
3. Name: LinuxGSM
4. Icon:
5. Copy the Webhook URL
6. Turn on discord alert and enter the URL in to the [LinuxGSM settings](../configuration/linuxgsm-config.md). (`~/lgsm/config-lgsm/<gameserver>/common.cfg`)

```
# Discord Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Discord
discordalert="on"
discordwebhook="https://discordapp.com/api/webhooks/3539332633367897009/5t_K4GkuBaR2-69TsKqXmHIya1ck1tirnu_Fst-DUC00dye98eaa_I6uTIcHEsi7a17K"
```

{% hint style="info" %}
You must have Discord _User Settings > Text & Images > Link Preview: 'Show website preview...'_ enabled or you will just see blank messages from the alert bot.
{% endhint %}
