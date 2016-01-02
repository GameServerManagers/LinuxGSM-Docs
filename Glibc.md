# Summary
Most servers require a specific version of Glibc installed. Newer distros normally have the required version. However the older the distro the less likely the server will run. Check the requirements below. If you have an older distro the game server may still run with a [Glibc fix](#glibc-fixes).

Server Requirements
===================
A more up to date list can be found here:
http://gameservermanagers.com/list/

A list of all the servers Glibc requirements

| Game Server                      | Glibc   |
|----------------------------------|---------|
| Ark: Survival Evolved            | 2.14    |
| 7 Days to Die                    | 2.15    |
| ARMA 3                           | 2.13    |
| Black Mesa: Deathmatch           | 2.07    |
| Blade Symphony                   | 2.15    |
| Counter Strike: Condition Zero   | 2.07    |
| Counter Strike: Global Offensive | 2.07    |
| Counter Strike 1.6               | 2.07    |
| Counter Strike: Source           | 2.07    |
| Day of Defeat                    | 2.07    |
| Day of Defeat: Source            | 2.07    |
| Deathmatch Classic               | 2.07    |
| Double Action: Boogaloo          | 2.15    |
| Fistful of Frags                 | 2.15    |
| Garry's Mod                      | 2.15    |
| Half Life: Deathmatch            | 2.07    |
| Half-Life: Opposing Force        | 2.07    |
| Half Life 2: Deathmatch          | 2.07    |
| Insurgency                       | 2.15    |
| Just Cause 2                     | 2.13    |
| Killing Floor                    | 2.07    |
| Left for Dead                    | 2.07    |
| Left for Dead 2                  | 2.07    |
| Mumble                           | n/a     |
| Natural Selection 2              | 2.15    |
| No More Room in Hell             | 2.15    |
| Project Zomboid                  | 2.15    |
| Red Orchestra: Ostfront 41-4     | 2.07    |
| Ricochet                         | 2.07    |
| Serious Sam 3:BFE                | 2.13    |
| Starbound                        | 2.12    |
| Team Fortress: Classic           | 2.07    |
| Team Fortress 2                  | 2.07    |
| Unreal Tournament 2004           | 2.00    |
| Unreal Tournament 99             | 2.00    |

Disto Glibc Versions
====================

List of distros and there Glibc version. 

http://distrowatch.com is also a great source to find this infomation.

| Distro           | Glibc   |
|------------------|---------|
| CentOS 6         | 2.12    |
| CentOS 7         | 2.17    |
| Debian 6         | 2.11.2  |
| Debian 7         | 2.13    |
| Debian 8         | 2.19    |
| Ubuntu 12.04 LTS | 2.15    |
| Ubuntu 14.04 LTS | 2.19    |

Glibc fixes
===========

> Many of the servers can work on distros with older _Glibc_ versions by using the _Glibc_ fixes that are available with LGSM. 

This simply copies the required files to the `serverfiles` directory. Many game servers will look for there dependencies in there `serverfiles` directory. Even if your dedicated server does not meet the Glibc requirement the server may still work.

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
A more up to date list can be found here:
http://gameservermanagers.com/list/

-   ARMA 3
-   Blade Symphony
-   Double Action: Boogaloo
-   Fistful of Frags
-   Garry's Mod
-   Insurgency
-   Just Cause 2
-   Natural Selection 2
-   NS2: Combat
-   No More Room in Hell
-   Serious Sam 3: BFE

No Glibc Fix available
----------------------
- 7 Days to Die
- Project Zomboid

External Links
==============

* [distrowatch.com](http://distrowatch.com/)
* [Glibc Homepage](http://www.gnu.org/software/libc/) 