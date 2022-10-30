# Java

Some game servers require using Java Runtime Environment (JRE) such as Minecraft and Project Zomboid.

## Installation of Java Runtime Environment

If you are unsure which version to choose simply pick the default JRE.

### Debian/Ubuntu

#### JRE

To install the most up to date JRE for the distro run:

```
apt install default-jre
```

#### OpenJRE

For `openjdk`, run the following changing the version number:

```
apt install openjdk-8-jre
```

```
apt install openjdk-11-jre
```

```
apt install openjdk-16-jre
```

```
apt install openjdk-17-jre
```

### CentOS

Run the following command, changing the version number:

```
yum install java-1.8.0-openjdk
```

```
yum install java-11-openjdk
```

## JRE Availability Table

JRE Availability Table Different Distros have different versions of Java. This page will outline the different versions that are available.

| Distro               | JRE 6 | JRE 7 | JRE 8 | JRE 11         | JRE 13 | JRE 16 | JRE 17 |
| -------------------- | ----- | ----- | ----- | -------------- | ------ | ------ | ------ |
| CentOS 7             | YES   | YES   | YES   | YES            | NO     | NO     | NO     |
| CentOS 8             | NO    | NO    | YES   | YES            | NO     | NO     | NO     |
| Debian 9 "Stretch"   | NO    | NO    | YES   | YES (backport) | NO     | NO     | NO     |
| Debian 10 "Buster"   | NO    | NO    | NO    | YES            | NO     | NO     | NO     |
| Debian 11 "Bullseye" | NO    | NO    | NO    | YES            | NO     | NO     | YES    |
| Ubuntu 16.04 LTS     | NO    | NO    | YES   | NO             | NO     | NO     | NO     |
| Ubuntu 18.04 LTS     | NO    | NO    | YES   | YES            | NO     | NO     | NO     |
| Ubuntu 20.04 LTS     | NO    | NO    | YES   | YES            | YES    | YES    | YES    |

[Distrowatch](https://distrowatch.com) also contains details of JRE versions.

Further Reading [https://help.ubuntu.com/community/Java](https://help.ubuntu.com/community/Java)
