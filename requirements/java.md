# Java

Some game servers require using Java Runtime Environment \(JRE\) such as Minecraft and Project Zomboid.

## Installation of Java Runtime Environment

If you are unsure which version to choose simply pick the default JRE.

### Debian/Ubuntu

#### JRE

To install the most up to date JRE for the distro run:

```text
apt install default-jre
```

#### OpenJRE

For `openjdk`, run the following changing the version number:

```text
apt install openjdk-8-jre
```

### CentOS/Fedora

Run the following command, changing the version number:

```text
yum install java-1.8.0-openjdk
```

## JRE Availability Table

JRE Availability Table Different Distros have different versions of Java. This page will outline the different versions that are available.

| Distro | JRE 6 | JRE 7 | JRE 8 | JRE 11 |
| :--- | :--- | :--- | :--- | :--- |
| CentOS 7 | YES | YES | YES | YES |
| CentOS 8 | NO | NO | YES | YES |
| Debian 8 | NO | YES | YES \(backport\) | NO |
| Debian 9 | NO | NO | YES | YES \(backport\) |
| Debian 10 | NO | NO | NO | YES |
| Ubuntu 16.04 LTS | NO | NO | YES | NO |
| Ubuntu 18.04 LTS | NO | NO | YES | YES |

[Distrowatch](https://distrowatch.com) also contains details of JRE versions.

Further Reading [https://help.ubuntu.com/community/Java](https://help.ubuntu.com/community/Java)

