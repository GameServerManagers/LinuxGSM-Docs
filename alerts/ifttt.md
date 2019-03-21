# IFTTT

![](../.gitbook/assets/ifttt_logo-1.png)

There are hundreds in integrations available on IFTTT allowing you to send alerts in all sorts of different ways to various services and devices.

## Setup IFTTT Webhook

To enable IFTTT you will need to setup a Webhooks integration.

1. Visit [https://ifttt.com/maker\_webhooks](https://ifttt.com/maker_webhooks)
2. Login and connect the Webhooks intergration
3. Select `Documentation` to get your IFTTT API key.
4. Paste the API key in to [LinuxGSM settings](../configuration/linuxgsm-config.md).

```text
# IFTTT Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/IFTTT
iftttalert="off"
ifttttoken="e-Yg8blVGDA15ewWvtZjUe"
iftttevent=""
```

## Create an IFTTT event name

An event name is a word used to trigger IFTTT event. This word is used when setting up an applet and can be any word you choose.

```text
# IFTTT Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/IFTTT
iftttalert="off"
ifttttoken="e-Yg8blVGDA15ewWvtZjUe"
iftttevent="linuxgsm_alert"
```

## Values

IFTTT allows 3 different values to be sent using the webhook; `Value1`, `Value2` and `Value3`. LinuxGSM sends different data for each value as listed below.

* Value1: Sends the servicename of the server e.g `csgoserver`
* Value2: Sends an alert subject e.g `Alert - csgoserver - Test`
* Value3: Sends an alert summary message.

```text
Testing LinuxGSM Alert. No action to be taken.
Game Squad
Server name LinuxGSM Server 1
Hostname ubuntu.example.com
Server IP 1.2.3.4:27015
```

## How to create an applet

1. Create a `New applet`
2. Select the `Webhooks` service
3. Choose `Receive a web request`
4. Enter your `Event Name` and click `Create Trigger`
5. Select an action service.
6. Give the applet a name and save.
