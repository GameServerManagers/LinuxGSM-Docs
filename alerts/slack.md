# Slack

![](../.gitbook/assets/slack_logo.png)

[Slack](https://slack.com) is a cloud-based set of proprietary team collaboration software tools and online services.

## Create a Discord Webhook

A webhook is required to post alerts to a slack.

1. Follow slack's guide to setting up an [incoming webhook](https://api.slack.com/incoming-webhooks).
2. Copy the Webhook URL
3. Turn on slack alerts and enter the URL in to the [LinuxGSM settings](../configuration/linuxgsm-config.md). \(`~/lgsm/config-lgsm/<gameserver>/common.cfg`\)

```text
# Slack Alerts | https://docs.linuxgsm.com/alerts/slack
slackalert="on"
slackwebhook="your webhook url"
```