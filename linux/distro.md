# distro

Picking a distro to run a game server is a personal choice and different admins have different preferences. There is no correct answer to which distro an individual chooses. However, there are some recommended choices when using LinuxGSM.

LinuxGSM developers primarily use Ubuntu for development and attempt to support the ones listed below. While LinuxGSM developers will attempt to support other distros there is no guarantee everything will work as expected, but should an issue occur, submitting GitHub issues is welcome.

## Ubuntu

![](../.gitbook/assets/ubuntu\_black-orange\_hex\_su.png)

Ubuntu is a free and open-source Linux distribution based on Debian, and popular with game developers such as Valve. Game developers tend to prefer newer software when developing game servers, as Ubuntu regularly release updates and have an LTS (Long-Term-Support) release every 2 years it is very compatible with game servers. Ubuntu has generally been known to have a large community and get relatively forgiving to newer users. Ubuntu is also the main choice of for the development of LinuxGSM. This means that Ubuntu is the recommended distro for LinuxGSM.

It is recommended that only Ubuntu LTS releases are used for game servers because of the longer support life span compared with standard releases (6 months). It is also recommended that the latest LTS is used when installing a server. If a server is currently running on an older LTS and the game server is functioning upgrading is optional.

{% hint style="info" %}
Ubuntu 18.04 LTS is recommended
{% endhint %}

| **Version**                                                                                                       | **Code name**    | **Release date** | **Supported until** |
| ----------------------------------------------------------------------------------------------------------------- | ---------------- | ---------------- | ------------------- |
| [~~16.04 LTS~~](https://en.wikipedia.org/wiki/List\_of\_Ubuntu\_releases#Ubuntu\_16.04\_LTS\_%28Xenial\_Xerus%29) | ~~Xenial Xerus~~ | ~~2016-04-21~~   | ~~2021-04~~         |
| [18.04 LTS](https://en.wikipedia.org/wiki/List\_of\_Ubuntu\_releases#Ubuntu\_18.04\_LTS\_%28Bionic\_Beaver%29)    | Bionic Beaver    | 2018-04-26       | 2028-04             |
| 20.04 LTS                                                                                                         | Focal Fossa      | 2020-04-23       | 2025-04             |

[https://en.wikipedia.org/wiki/Ubuntu#Releases](https://en.wikipedia.org/wiki/Ubuntu#Releases)

## Debian

![](../.gitbook/assets/debian.png)

Debian is another popular distro that sits upstream of Ubuntu that shares many of the same advantages of Ubuntu. The release cycle is every 2 years. Debian supports “backports”, which allows newer software to be installed on stable Debian releases. This is particularly useful for game servers and LinuxGSM that may require newer software.

{% hint style="info" %}
Debian 10 "Buster" is recommended
{% endhint %}

| **Version** | **Status**       | **Code name** | **Release date**     | **Security support until** | **LTS until**    |
| ----------- | ---------------- | ------------- | -------------------- | -------------------------- | ---------------- |
| ~~8~~       | ~~oldoldstable~~ | ~~Jessie~~    | ~~25–26 April 2015~~ | ~~17 June 2018~~           | ~~30 June 2020~~ |
| 9           | oldstable        | Stretch       | 17 June 2017         | 2020                       | June 2022        |
| 10          | stable           | Buster        | 6 July 2019          | 2022                       | 2024             |

[https://en.wikipedia.org/wiki/Debian\_version\_history#Release\_table](https://en.wikipedia.org/wiki/Debian\_version\_history#Release\_table)

## CentOS

![](../.gitbook/assets/centos.png)

CentOS is a Linux distribution that provides a free, enterprise-class, community-supported computing platform functionally compatible with its upstream source, Red Hat Enterprise Linux. This means CentOS is considered a very stable enterprise-grade distro and as such is very popular with server admins. CentOS also has a very long support cycle compared with other distros. The main downside to stability is that the latest software is not always available; this can be an issue when dealing with game servers.

{% hint style="danger" %}
[Significant changes](https://blog.centos.org/2020/12/future-is-centos-stream/) in the future of CentOS has occured.
{% endhint %}

{% hint style="warning" %}
CentOS 6 is not supported by LinuxGSM
{% endhint %}

{% hint style="info" %}
CentOS 8 is recommended
{% endhint %}

| **CentOS version** | Release date      | Full updates    | Maintenance updates  |
| ------------------ | ----------------- | --------------- | -------------------- |
| ~~6~~              | ~~10 July 2011~~  | ~~10 May 2017~~ | ~~30 November 2020~~ |
| 7                  | 7 July 2014       | 6 August 2020   | 30 June 2024         |
| 8                  | 24 September 2019 | 1 May 2024      | 31 December 2021     |
| Stream 8           |                   |                 | 31 May 2024          |

### EPEL

LinuxGSM uses packages that are not available by default in CentOS because of this the EPEL (Extra Packages for Enterprise Linux) repository is required to install all dependencies. EPEL is a repository managed by the fedora project to add extra packages to RHEL/CentOS.

{% hint style="info" %}
EPEL is required to run LinuxGSM
{% endhint %}
