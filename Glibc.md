# Summary
Most servers require a specific version of Glibc installed. Newer distros normally have the required version. However the older the distro the less likely the server will run. Check the requirements below. If you have an older distro the game server may still run with a [Glibc fix](#glibc-fixes).

Server Requirements
===================
A complete list can be found here:

https://gameservermanagers.com/list/

Distro Glibc Versions
====================
List of distros and there Glibc version. 

| Distro           | Glibc   |
|------------------|---------|
| CentOS 5         | 2.5     |
| CentOS 6         | 2.12    |
| CentOS 7         | 2.17    |
| Debian 6         | 2.11.2  |
| Debian 7         | 2.13    |
| Debian 8         | 2.19    |
| Debian 9         | 2.23    |
| Ubuntu 12.04 LTS | 2.15    |
| Ubuntu 14.04 LTS | 2.19    |
| Ubuntu 16.04 LTS | 2.23    |

[distrowatch.com](http://distrowatch.com) is also a great source to find this information. 

Glibc version history available on [Wikipedia](https://en.wikipedia.org/wiki/GNU_C_Library#Version_history).

Glibc fixes
===========

> Many of the servers can work on distros with older _Glibc_ versions by using the _Glibc_ fixes that are available with LGSM. 

If your distro does not meet the Glibc requirements LGSM will download the glibc files to the lgsm/lib directory to be used by the game server. Because of this even if your dedicated server does not meet the Glibc requirements the game server should still work.

These fixes prevent errors similar to the following:
```
version `GLIBC_2.15′ not found
```   
```
./7DaysToDie.x86: /usr/lib/libstdc++.so.6: version GLIBCXX_3.4.15 not found (required by ./7DaysToDie.x86)
./7DaysToDie.x86: /lib/libc.so.6: version GLIBC_2.15 not found (required by ./7DaysToDie.x86)
./7DaysToDie.x86: /lib/libm.so.6: version GLIBC_2.15 not found (required by ./7DaysToDie.x86)
```

Glibc Fix available
-------------------
List of game servers with glibc fixes:

https://gameservermanagers.com/list/

No Glibc Fix available
----------------------
Some game servers to not work with Glibc Fixes:

https://gameservermanagers.com/list/

External Links
==============

* [distrowatch.com](http://distrowatch.com/)
* [Glibc Homepage](http://www.gnu.org/software/libc/) 