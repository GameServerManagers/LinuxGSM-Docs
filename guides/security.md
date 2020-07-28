# Security

TO-DO

## Avoid a security breach and allow you to run multiple servers

{% hint style="danger" %}
needs to be verified
{% endhint %}

By default, a user can see all started processes from other users, which is bad, but also their start parameters, which is pretty dangerous. Those start parameters can contain sensitive information, such as RCON password, Steam API keys and GSLT upon start, a Rust dedicated server is checking if the process name started by any user, and will prevent you from running it again if it finds it, displaying "Player is already running".

To avoid that, run:

```bash
mount -o remount,rw,hidepid=2 /proc
```

And to keep the changes upon machine reboot:

```bash
nano /etc/fstab
# Here are the modification to apply to the "proc" line
proc    /proc    proc    defaults,hidepid=2    0    0
```

You still need to make one user per server, change ports, and repeat the install process. \(See [this](../features/multiple-game-servers.md) for more info\)

