# MQTT

[MQTT](https://mqtt.org) is a lightweight publish and subscribe messaging protocol. LinuxGSM can publish each alert to an MQTT broker, so tools like Home Assistant, Node-RED and openHAB can react to your game servers.

## Requirements

- An MQTT broker you can reach from the game server, for example [Mosquitto](https://mosquitto.org).
- The `mosquitto_pub` client. LinuxGSM installs it for you when MQTT alerts are on: `mosquitto-clients` on Debian and Ubuntu, `mosquitto` on CentOS, Rocky, AlmaLinux and Fedora.

## Configuring MQTT Alerts

1. **Turn on MQTT alerts** in the [LinuxGSM settings](../configuration/linuxgsm-config.md). \(`lgsm/config-lgsm/<gameserver>/common.cfg`\)
2. **Set your broker details.** Host, port and topic are required. Username and password are only needed if your broker uses authentication.
3. Run `./<gameserver> test-alert` and check your subscriber received the message.

```text
# MQTT Alerts | https://docs.linuxgsm.com/alerts/mqtt
mqttalert="on"
mqtthost="mqtt.example.com"
mqttport="1883"
mqttuser=""
mqttpassword=""
mqtttopic="lgsm/alerts"
mqtttls="off"
```

| Setting        | Default            | Description                                                      |
| -------------- | ------------------ | ---------------------------------------------------------------- |
| `mqttalert`    | `off`              | Set to `on` to enable MQTT alerts.                               |
| `mqtthost`     | `mqtt.example.com` | Broker hostname or IP address.                                   |
| `mqttport`     | `1883`             | Broker port. Use `8883` for TLS.                                 |
| `mqttuser`     |                    | Username, if the broker needs one.                               |
| `mqttpassword` |                    | Password, if the broker needs one.                               |
| `mqtttopic`    | `lgsm/alerts`      | Topic to publish to. Use a different topic for each game server. |
| `mqtttls`      | `off`              | Set to `on` to connect over TLS using the system certificates.   |

{% hint style="info" %}
Don't start the topic with a `/`. MQTT treats `/lgsm` and `lgsm` as different topics.
{% endhint %}

## Message Format

Each alert is one JSON message:

```json
{
  "title": "Restarted - My Rust Server",
  "message": "rustserver has been restarted.",
  "server": "My Rust Server",
  "game": "Rust",
  "hostname": "gameserver01",
  "ip": "203.0.113.10:28015",
  "url": "",
  "time": "Thu 12 Nov 21:41:40 GMT 2026"
}
```

`url` is only filled when `postalert="on"` ([More info](README.md#more-info)).

## Testing

Subscribe to the topic from any machine with the Mosquitto clients installed:

```bash
mosquitto_sub -h mqtt.example.com -t 'lgsm/alerts'
```

Then send a test alert:

```bash
./<gameserver> test-alert
```

{% hint style="warning" %}
`mosquitto_pub` takes the password as a command line argument, so other users on the same machine could see it in the process list while an alert is sending. Use a broker account that can only publish to your LinuxGSM topic.
{% endhint %}
