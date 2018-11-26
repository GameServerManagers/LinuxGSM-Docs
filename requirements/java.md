# Java

Some game servers require using Java Runtime Environment \(JRE\) such as Minecraft and Project Zomboid.

## Installation of Java Runtime Environment

### Debian/Ubuntu

To install the most up to date JRE for your distro run the following: `apt install default-jre` Or to select openjdk, run the following changing the version number: `apt install openjdk-8-jre`

Alternatively on Ubuntu you can use webupd8 PPA to download and install Oracle's Java. This is required for some Java profiling tools as those tools only use Oracle's JDK. You can view the instructions on how [here](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html) Debian can follow webupd8 guide [here](http://www.webupd8.org/2014/03/how-to-install-oracle-java-8-in-debian.html)

### CentOS/Fedora

Run the following command, changing the version number:

```text
yum install java-1.8.0-openjdk
```

## JRE Availability Table

JRE Availability Table Different Distros have different versions of Java. This page will outline the different versions that are available.

| Distro | JRE 6 | JRE 7 | JRE 8 |
| :--- | :--- | :--- | :--- |
| CentOS 5 | YES | YES | NO |
| CentOS 6 | YES | YES | YES |
| CentOS 7 | YES | YES | YES |
| Debian 6 | YES | NO | NO |
| Debian 7 | YES | YES | NO |
| Debian 8 | NO | YES | YES \(backport\) |
| Debian 9 | NO | NO | YES |
| Ubuntu 12.04 LTS | YES | YES | NO |
| Ubuntu 14.04 LTS | YES | YES | NO |
| Ubuntu 16.04 LTS | NO | NO | YES |
| Ubuntu 18.04 LTS | NO | NO | YES |

[Distrowatch](https://distrowatch.com) also contains details of JRE versions.

Further Reading [https://help.ubuntu.com/community/Java](https://help.ubuntu.com/community/Java)

