# tmux

LinuxGSM uses tmux to run servers in the background so the instance is not lost when you close a terminal session.

Tmux is a key component of LinuxGSM and replaced [screen](http://en.wikipedia.org/wiki/GNU_Screen) which was used on earlier versions. tmux has a few improvements over screen; mainly being better at handling standard Linux users, this was a major issue when developing with screen. tmux allows LinuxGSM to call up a game server running in the background so you can see what it is doing; this feature is available with [console](../commands/console.md) feature.

> LinuxGSM requires _tmux =&gt; 1.6_ to enable console logging.

### tmuxception

Some server admins have attempted to run LinuxGSM within a `tmux` or `screen` session. It is As LinuxGSM calls tmux is is not possible to run LinuxGSM within a tmux or screen session

You cannot run a tmux session inside another tmux session or inside of a screen session.

## Known Issues

### Tmux 1.8

tmux 1.8 has an issue that prevents console logging from working. This is because the `pipe-pane` feature is broken in tmux 1.8 causing it not to output the console to the console log files. The only solution is to use another version of tmux.

## create session failed: Operation not permitted

This issue occurs on CentOS mainly. This is caused by the standard user not having permissions to user _/dev/ptmx_.

```text
create session failed: ./srcds_linux -game csgo: Operation not permitted
```

To fix this the user needs to be part of the _tty_ group.

```text
usermod -G tty csgoserver
```

To check the user has been added check _/etc/group_.

```text
grep tty /etc/group
```

```text
tty:x:5:csgoserver
```

## Installing the latest tmux CentOS 7 using Ghettoforge

If you are using an older version of tmux on CentOS you can upgrade to the latest version by installing the [Ghettoforge](http://ghettoforge.org) repository.

Install Ghettoforge with the following command.

```text
yum install http://mirror.ghettoforge.org/distributions/gf/gf-release-latest.gf.el7.noarch.rpm
```

Install tmux using the Ghettoforge repo.

```text
yum --enablerepo=gf-plus install tmux
```

Once installed restart the server.

### External links

[https://tmux.github.io](https://tmux.github.io/)

