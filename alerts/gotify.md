# Gotify

[Gotify](https://gotify.net) is a self-hosted server for sending and receiving messages. Alerts sent to Gotify can be received in the Gotify web UI, the Android app, or any client that uses the Gotify API.

## Create an application

LinuxGSM sends alerts to Gotify as an application, and needs that application's token.

1. Log in to the Gotify web UI.
2. Open the **Apps** tab and click **Create Application**.
3. Give it a name, such as `LinuxGSM`, and click **Create**.
4. Copy the token shown for the new application.

## Enable Gotify alerts

Turn on Gotify alerts and enter your details in the [LinuxGSM config](../configuration/linuxgsm-config.md) (`~/lgsm/config-lgsm/<gameserver>/common.cfg`).

```bash
# Gotify Alerts | https://docs.linuxgsm.com/alerts/gotify
gotifyalert="on"
gotifytoken="AbCdEf1234567890"
gotifywebhook="https://gotify.example.com"
```

| Setting | Description |
|---|---|
| `gotifyalert` | Set to `on` to enable Gotify alerts. |
| `gotifytoken` | The application token from the Gotify web UI. |
| `gotifywebhook` | The base URL of your Gotify server, without a trailing `/` or `/message`. LinuxGSM adds `/message` itself. |

Alerts are sent with priority 5.

## Testing the configuration

Execute a test alert with `./gameserver test-alert` to verify the setup. If the alert appears in Gotify, the configuration is correct.
