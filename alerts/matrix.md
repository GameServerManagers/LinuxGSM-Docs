# Matrix

![](../.gitbook/assets/matrix_logo.png)

[Matrix](https://matrix.org/) is an open network for secure, decentralized communication that allows to allows other applications to send messages via an API.

## Setup a Matrix Bot

To enable Matrix alerts, it is recommended that you create a new account dedicated to sending alerts. This will act as a bot account. You can create an account on your preferred Matrix server. Once you create your account, you can assign it a friendly name and a [picture](https://raw.githubusercontent.com/n194/LinuxGSM/matrix-alert/lgsm/data/alert_discord_logo.jpg).

Next, you will have to get an access token for the account. 
- Element: https://t2bot.io/docs/access_tokens/
- API: https://www.matrix.org/docs/guides/client-server-api#login

Enter your homeservers and the token in the [LinuxGSM config](../configuration/linuxgsm-config.md).

```text
   #Matrix Alerts | https://docs.linuxgsm.com/alerts/matrix
   matrixalert="on"
   matrixhomeserver="matrix.org"
   matrixtoken="swt_a219dC4ib5T_QjAZsnEPpJLDNWSeDfk_8vj1Uw"
   matrixroom=""
```

## Matrix room ID

The room ID is used to identify where the alert is being sent. Each room has its own unique ID.

To obtain the room ID in Element, go to the room settings, go to the advanced tab and copy the internal room ID.

Add the room id to the [LinuxGSM config](../configuration/linuxgsm-config.md).

```text
   #Matrix Alerts | https://docs.linuxgsm.com/alerts/matrix
   matrixalert="on"
   matrixhomeserver="matrix.org"
   matrixtoken="swt_a219dC4ib5T_QjAZsnEPpJLDNWSeDfk_8vj1Uw"
   matrixroom="!ygKaCNBxvTMUSagvZdz:matrix.org"
```
8080
### Send Test Alert

Finally, test that everything correctly works by sending a test alert. You will now receive a message from the bot directly or to a chosen group.

```text
./gameserver test-alert
```
