# Gotify

![](../.gitbook/assets/gotify-logo.png)

[Gotify](https://gotify.net/) is a simple server for sending and receiving messages. A good way to look at it is as a selfhosted version of [pushover](https://pushover.net/) or [pushbullet](https://www.pushbullet.com/).

## Creating your app within gotify

To send messages from LGSM, we'll need to setup an app within Gotify first.  
Once logged in, click on `apps` and `create new app`.  
Choose a name and then copy the token as we'll need that later.

## Configuring LGSM to use Gotify alerts

Next up, it's time to update the [server config](../configuration/linuxgsm-config#common-cfg).

```
# Gotify Alerts | https://docs.linuxgsm.com/alerts/gotify
gotifyalert="on"
gotifytoken="token"
gotifywebhook="webhook"
```

### Gotifytoken

This is where you'll want to put your token you got when making the app within Gotify.

### Gotifywebhook

If the full URL for your Gotify instance is `example.com`, here's what your gotify webhook would look like: `https://example.com/message`

## Send Test Alert

Time to test and start receiving your alerts!

```
./gameserver test-alert
```
