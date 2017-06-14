# Summary
Most servers require a specific version of glibc installed. Newer distros normally have the required version. However the older the distro the less likely the server will run. Check the requirements below. If you have an older distro the game server may still run with a [glibc fix](#glibc-fixes).

Server Requirements
===================
A complete list can be found here:

https://gameservermanagers.com/list/

Distro glibc Versions
====================
List of distros and there glibc version. 

| Distro           | glibc   |
|------------------|---------|
| CentOS 5         | 2.5     |
| CentOS 6         | 2.12    |
| CentOS 7         | 2.17    |
| Fedora 17        | 2.15    |
| Fedora 18        | 2.16    |
| Fedora 19        | 2.17    |
| Fedora 20        | 2.18    |
| Debian 6         | 2.11.2  |
| Debian 7         | 2.13    |
| Debian 8         | 2.19    |
| Debian 9         | 2.24    |
| Ubuntu 12.04 LTS | 2.15    |
| Ubuntu 14.04 LTS | 2.19    |
| Ubuntu 16.04 LTS | 2.23    |

[distrowatch.com](http://distrowatch.com) is also a great source to find this information. 

glibc version history available on [Wikipedia](https://en.wikipedia.org/wiki/GNU_C_Library#Version_history).

glibc fixes
===========

> Many of the servers can work on distros with older _glibc_ versions by using the _glibc_ fixes that are available with LinuxGSM. 

If your distro does not meet the glibc requirements LinuxGSM will download the glibc files to the `lgsm/lib` directory to be used by the game server. Because of this even if your dedicated server does not meet the glibc requirements the game server should still work.

These fixes prevent errors similar to the following:
```
version `glibc_2.15′ not found
```   
```
./7DaysToDie.x86: /usr/lib/libstdc++.so.6: version glibcXX_3.4.15 not found (required by ./7DaysToDie.x86)
./7DaysToDie.x86: /lib/libc.so.6: version glibc_2.15 not found (required by ./7DaysToDie.x86)
./7DaysToDie.x86: /lib/libm.so.6: version glibc_2.15 not found (required by ./7DaysToDie.x86)
```

glibc Fix available
-------------------
List of game servers with glibc fixes:

https://gameservermanagers.com/list/

No glibc Fix available
----------------------
Some game servers to not work with glibc Fixes:

https://gameservermanagers.com/list/

External Links
==============

* [distrowatch.com](http://distrowatch.com/)
* [glibc Homepage](http://www.gnu.org/software/libc/) 