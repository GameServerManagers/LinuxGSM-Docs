# Matrix

[Matrix](https://matrix.org) is an open standard for decentralised, real-time communication. LinuxGSM uses the [Matrix Client-Server API](https://spec.matrix.org/latest/client-server-api/) to send alerts to a room on any Matrix homeserver (matrix.org or self-hosted).

## Create a room for alerts

Create a room for LinuxGSM to post alerts into using any Matrix client (e.g. [Element](https://element.io)).

{% hint style="warning" %}
Create the room with **encryption disabled**. LinuxGSM sends alerts as plain messages over the Client-Server API and does not support end-to-end encryption. In an encrypted room, alerts will still arrive but show as unverified/unencrypted with a warning. Encryption cannot be turned off once a room has been created, so choose this when creating the room (in Element: _Add room > uncheck "Enable end-to-end encryption"_).
{% endhint %}

## Get your access token

An access token authenticates LinuxGSM as your Matrix account.

In Element: _Settings > Help & About > Advanced > Access Token_ and click to reveal, then copy it.

{% hint style="info" %}
An access token grants full access to your Matrix account. Consider creating a dedicated account for alerts rather than using your personal one, and treat the token like a password.
{% endhint %}

## Get the room ID

LinuxGSM needs the room's **internal room ID**, which starts with `!` (e.g. `!wsxanjDijPztgZgrYL:matrix.org`).

{% hint style="warning" %}
Use the internal **room** ID (`!...:server`), not a room **alias** (`#room:server`) and not a **space** ID. A space is a container for rooms, not a room you can post to — its ID will look like a room ID but sending to it will fail. In Element, find the internal room ID under _Room Settings > Advanced > Internal room ID_.
{% endhint %}

## Enable Matrix alerts

Turn on Matrix alerts and enter your details in the [LinuxGSM config](../configuration/linuxgsm-config.md) (`~/lgsm/config-lgsm/<gameserver>/common.cfg`).

```bash
# Matrix Alerts | https://docs.linuxgsm.com/alerts/matrix
matrixalert="on"
matrixhomeserver="matrix.org"
matrixtoken="mat_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
matrixroom="!wsxanjDijPztgZgrYL:matrix.org"
```

| Setting | Description |
|---|---|
| `matrixalert` | Set to `on` to enable Matrix alerts. |
| `matrixhomeserver` | Your homeserver. A bare hostname is assumed to be `https://`; `http://`/`https://` prefixes are respected. |
| `matrixtoken` | Your account access token. |
| `matrixroom` | The internal room ID (`!...:server`) to send alerts to. |

{% hint style="info" %}
If your homeserver uses `.well-known` delegation (matrix.org delegates to `matrix-client.matrix.org`), the bare domain works in most cases. If alerts fail to send, try setting `matrixhomeserver` to the delegated client API host directly.
{% endhint %}

## Testing the configuration

Execute a test alert with `./gameserver test-alert` to verify the setup. If the alert appears in your Matrix room, the configuration is correct.
