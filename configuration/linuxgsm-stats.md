# LinuxGSM Stats

LinuxGSM Stats is an optional, opt-in report that helps the project see which game servers and Linux distributions people use. Stats are off by default.

## Enable Stats

Add `stats="on"` to your [LinuxGSM config](linuxgsm-config.md), such as `common.cfg` for every instance or an instance config for one server. You can also opt in during installation. Set `stats="off"` to stop future reports.

## What Is Sent

The report contains:

- A randomly generated instance UUID, so reports from the same server instance can be grouped.
- Game name, Linux distribution, LinuxGSM version and virtualisation type.
- CPU core count, total RAM and disk capacity.
- Game server CPU, RAM and disk use when those values are available and above zero. CPU use is rounded up to 100 MHz and RAM use to 100 MB.
- Names of enabled alert types, such as Discord or email. No alert address or token is included.

The report does not include the CPU model, machine ID, hostname, server IP address, alert destinations or credentials. The collector receives the network connection used to send the report, as any web service does.

The UUID is stored in `lgsm/data/uuid-<instance>.txt`. Only the random UUID portion is sent, without the human-readable name prefix. Removing the UUID files causes LinuxGSM to generate new identifiers on a later stats run.

## When and Where It Is Sent

LinuxGSM sends a report to `https://usage.linuxgsm.com/v1/report` at most once per day for each instance when stats run. It no longer sends stats to Google Analytics. The request has a five-second timeout and a collector failure does not stop the server or delay monitoring beyond that timeout.

The data helps prioritise LinuxGSM development and is used in the [public usage dashboard](https://linuxgsm.com/data/usage/).

You can inspect how the report is built in [`info_stats.sh`](https://github.com/GameServerManagers/LinuxGSM/blob/develop/lgsm/modules/info_stats.sh).
