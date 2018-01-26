
LinuxGSM uses tmux to run servers in the background so the instance is not lost when you close a terminal session.

Tmux is a key component of LinuxGSM and replaced [screen] which was used on earlier versions. tmux has a few improvements over screen; mainly being better at handling of non root users which was a major issue when developing with screen. tmux allows LinuxGSM to call up a game server running in the background so you can see what it is doing; this feature is available with [[console]] feature.

> LinuxGSM requires _tmux =\> 1.6_ to enable console logging.

tmuxception
-----------
You cannot run a tmux session inside another tmux session or inside of a screen session.

Known Issues
========

Tmux 1.8
--------
tmux 1.8 has an issue that prevents console logging from working. This is because the `pipe-pane` feature is broken in tmux 1.8 causing is not to output the console to the console log files. The only solution is to use another version of tmux.

### Upgrade Tmux CentOS (7)

[Upgrade Tmux on CentOS](Tmux#installing-the-latest-tmux-from-source-on-centos-7)

### Upgrade Tmux Ubuntu

http://stackoverflow.com/a/25952511

Here are the steps to update Ubuntu - version 14.04 only (see below for other ubuntu versions):

    sudo apt-get update

    sudo apt-get install -y python-software-properties software-properties-common

    sudo add-apt-repository -y ppa:pi-rho/dev

    sudo apt-get update

    sudo apt-get install -y tmux=2.0-1~ppa1~t


If you have another ubuntu version you might want to install a different tmux version from the same repo. So:

ubuntu 12.04 (Precise Pangolin) step 5: `sudo apt-get install -y tmux=1.9a-1~ppa1~p `(installs tmux 1.9)

ubuntu 13.10 (Saucy Salamander) step 5: `sudo apt-get install -y tmux=1.9a-1~ppa1~s` (installs tmux 1.9)

ubuntu 14.10 (Utopic Unicorn) step 5: `sudo apt-get install -y tmux=2.0-1~ppa1~u`

ubuntu 15.04 (Vivid Vervet) step 5: `sudo apt-get install -y tmux=2.0-1~ppa1~v`


create session failed: Operation not permitted
==============================================
This issue occurs on CentOS mainly. This is caused by the standard user not having permissions to user _/dev/ptmx_.
```
create session failed: ./srcds_linux -game csgo: Operation not permitted
```

To fix this the user needs to be part of the _tty_ group.

```
usermod -G tty csgoserver
```
To check the user has been added check _/etc/group_.
```
grep tty /etc/group
```
```
tty:x:5:csgoserver
```
# Installing the latest tmux CentOS 7 using Ghettoforge
If you are using an older version of tmux on CentOS you can upgrade to the latest version by installing the [Ghettoforge](http://ghettoforge.org) repository.

1. ```wget http://mirror.ghettoforge.org/distributions/gf/gf-release-latest.gf.el7.noarch.```
2. ```rpm -Uvh gf-release*rpm```
3. ```yum --enablerepo=gf-plus install tmux```


## Note on live servers

You can install tmux while the server are running, however restarting/stopping them will not be possible

You can do either of the following possibilities

* Stop all servers before upgrading tmux
* Upgrade tmux while servers are running, but you must kill the tmux processes to be able to start a new one running the latest version
* Manually attach the running tmux and manually shut it down.

External links
--------------

[tmux Homepage][]

  [LGSM Console using tmux]: Tmux.PNG‎ "fig:LGSM Console using tmux"
  [screen]: http://en.wikipedia.org/wiki/GNU_Screen
  [tmux Homepage]: https://tmux.github.io/