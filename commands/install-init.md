# install-init
The `install-init` command can generate the contents from a systemd service file and place the contents automatically into `/etc/systemd/system`

The naming conventions are the short name of the server (e.g. `mcserver` as minecraft server) plus `-lgsm.service`

See [running on boot](../configuration/running-on-boot.md) for more information.

## Commands

Run the following command to install the systemd service files:

Standard: `./gameserver install-init`
Short: `./gameserver ii`

Then enter your root password.

## Example output

```
[  OK  ] systemd service file mcserver: Generated the file contents
Information! Enter the password of root:
Password:
Complete! Placed the file in /etc/systemd/system/ as mcserver-lgsm.service
Information! run `systemctl enable mcserver-lgsm.service` (as root), to enable the game on boot
```
