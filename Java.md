Some game servers require using Java Runtime Environment (JRE) such as Minecraft and Project Zomboid. 

<h1>Installation of Java Runtime Environment</h1>

<h2>Debian/Ubuntu</h2>
To install the most up to date JRE for your distro run the following:

     apt install default-jre

Or to select run the following changing the version number:

    apt install openjdk-8-jre

 <h2>CentOS/Fedora</h2>

Run the following command, changing the version number:

    yum install java-1.8.0-openjdk

<h1>JRE Availability Table</h1>
Different Distros have different versions of Java. This page will outline the different versions that are available.

| Distro           |JRE 6|JRE 7|JRE 8|
|------------------|-----|-----|-----|
| CentOS 5         | YES | YES | NO  |
| CentOS 6         | YES | YES | YES |
| CentOS 7         | YES | YES | YES |
| Debian 6         | YES | NO  | NO  |
| Debian 7         | YES | YES | NO  |
| Debian 8         | NO  | YES | YES (backport)|
| Debian 9         | NO  | NO  | YES |
| Ubuntu 12.04 LTS | YES | YES | NO  |
| Ubuntu 14.04 LTS | YES | YES | NO  |
| Ubuntu 16.04 LTS | NO  | NO  | YES |

[Distrowatch](https://distrowatch.com) also contains details of JRE versions.

<h1>Further Reading</h1>
https://help.ubuntu.com/community/Java
