# ANSI Colors

LinuxGSM uses colours and in-place progress messages when stdout is an interactive terminal. The default setting is `ansi="on"`.

When stdout is a pipe, redirected file, systemd journal, cron log or container log, LinuxGSM automatically prints plain, complete lines. It omits colours, text styles, carriage returns and erase-line sequences. This makes captured output readable without changing your terminal display.

Set `ansi="off"` in your [LinuxGSM config](../configuration/linuxgsm-config.md) to disable ANSI formatting in an interactive terminal too. Terminal progress messages can still update in place with a carriage return.

This setting applies to LinuxGSM's own messages. Output produced directly by a game server or SteamCMD can have its own formatting.
