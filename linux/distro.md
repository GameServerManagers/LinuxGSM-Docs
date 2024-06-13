# distro

Picking a distro to run a game server is a personal choice and different admins have different preferences. There is no correct answer to which distro an individual chooses. However, there are some recommended choices when using LinuxGSM.

LinuxGSM developers primarily use Ubuntu for development and attempt to support the ones listed below. While LinuxGSM developers will attempt to support other distros there is no guarantee everything will work as expected, but should an issue occur, submitting GitHub issues is welcome.

## Debian Based Distributions

### Ubuntu

![](../.gitbook/assets/ubuntu\_black-orange\_hex\_su.png)

#### **Reasons to use Ubuntu with LinuxGSM:**

1. **Stability and Reliability:** Ubuntu is a free and open-source Linux distribution based on Debian. It is renowned for its stability and reliability, making it an excellent choice for hosting game servers. Ubuntu's LTS (Long-Term Support) releases, which are published every two years, offer an extended support lifespan, ensuring that your server remains secure and up-to-date for an extended period.
2. **Game Developer Preference:** Ubuntu has gained popularity among game developers and companies like Valve. This preference is due to Ubuntu's consistent and timely software updates, allowing game developers to work with newer libraries and tools, which is essential for developing and running modern game servers.
3. **Large and Supportive Community:** With a vast user base, Ubuntu boasts an active and helpful community. This large community ensures that you can easily find solutions to issues, access guides, and receive support when setting up or troubleshooting your game server.
4. **User-Friendly Experience:** Ubuntu is known for its user-friendly interface, making it an attractive choice for both experienced Linux users and newcomers. The distribution provides an intuitive environment, simplifying the server setup process for those who might be new to managing game servers.
5. **Preferred Distro for LinuxGSM Development:** Ubuntu is the main choice for the development of LinuxGSM itself. Using Ubuntu ensures that you have the best compatibility and the smoothest experience when running LinuxGSM for managing your game servers.

#### **Recommendations for Ubuntu Usage with LinuxGSM:**

1. **Choose LTS Releases:** It is highly recommended to use Ubuntu LTS releases for hosting game servers. LTS releases offer a longer support lifespan (typically 5 years) compared to standard releases (which have a support period of 6 months). This longer support period means fewer disruptions and security risks for your game server.
2. **Latest LTS Version:** Whenever you install a game server, opt for the latest LTS release available at that time. This ensures that you have access to the latest software and updates, maximizing compatibility and security.
3. **Optional Upgrades:** If your game server is currently running on an older LTS release and is functioning correctly, upgrading to a newer LTS release is optional. However, consider upgrading at an appropriate time to stay current with the latest features and security patches.

{% hint style="info" %}
Ubuntu 22.04 LTS is recommended
{% endhint %}

| **Version** | **Code name**   | **Release date** | **Supported until** |
| ----------- | --------------- | ---------------- | ------------------- |
| 20.04 LTS   | Focal Fossa     | 2020-04-23       | 2025-04             |
| 22.04 LTS   | Jammy Jellyfish | 2022-04-21       | 2027-04             |

[https://en.wikipedia.org/wiki/Ubuntu#Releases](https://en.wikipedia.org/wiki/Ubuntu#Releases)

### Debian

![](../.gitbook/assets/debian.png)

#### **Reasons to use Debian with LinuxGSM:**

1. **Rock-Solid Stability:** Debian is renowned for its unmatched stability and reliability. As the upstream distribution for Ubuntu, it serves as the foundation for many popular Linux distributions, including Ubuntu itself. For game servers that require a stable and consistent environment, Debian is an excellent choice.
2. **Long Release Cycle:** Debian follows a predictable release cycle, with major stable releases approximately every two years. This extended cycle ensures a robust and mature platform for hosting game servers, minimizing the need for frequent system updates and reconfigurations.
3. **Backports Support:** One of Debian's significant advantages is the availability of "backports." These are newer versions of software packages that can be installed on stable Debian releases. This feature allows you to access the latest software and libraries that might be required for running specific game servers and LinuxGSM.
4. **Wide Package Selection:** Debian boasts a vast repository of software packages, covering a broad range of applications and tools. This extensive selection ensures that you can easily find and install the necessary dependencies and server components to run your game servers smoothly.
5. **Security Focus:** Security is a top priority for Debian's development team. The distribution is known for its prompt security updates and active maintenance, making it a secure choice for hosting game servers and protecting them from potential threats.

#### **Recommendations for Debian Usage with LinuxGSM:**

1. **Stable Releases:** For most game server deployments, it is recommended to use Debian's stable releases. These versions have undergone extensive testing and are well-suited for production environments.
2. **Backports for Newer Software:** If your game server or LinuxGSM requires newer software versions, consider using the backports repository. This way, you can leverage the latest software while still benefiting from Debian's overall stability.
3. **Security Updates:** Regularly apply security updates to keep your Debian server secure and protected from potential vulnerabilities. Debian's robust security team ensures that security patches are promptly released and widely available.
4. **Consider System Requirements:** Before choosing Debian, ensure that your game server's software and any specific tools you intend to use are compatible with the version of Debian you plan to install. Verify system requirements to ensure optimal performance.

{% hint style="info" %}
Debian 12 "Bookworm" is recommended
{% endhint %}

[https://en.wikipedia.org/wiki/Debian\_version\_history](https://en.wikipedia.org/wiki/Debian\_version\_history)

| **Version** | **Status**       | **Code name** | **Release date** | **Security support until** | **LTS until** |
| ----------- | ---------------- | ------------- | ---------------- | -------------------------- | ------------- |
| 10          | ~~oldoldstable~~ | Buster        | 6 July 2019      | 2022                       | 2024          |
| 11          | oldstable        | Bullseye      | 14 August 2021   |                            |               |
| 12          | stable           | Bookworm      | 10 June 2023     |                            |               |

[https://en.wikipedia.org/wiki/Debian\_version\_history#Release\_table](https://en.wikipedia.org/wiki/Debian\_version\_history#Release\_table)

## Enterprise Linux Distros

LinuxGSM also works with Enterprise Linux distributions. Known for their stability and long support cycle Enterprise Linux distros are a great choice for Game Servers

### CentOS

![](../.gitbook/assets/centos.png)

{% hint style="info" %}
CentOS is no longer recommended for use with LinuxGSM for hosting game servers.
{% endhint %}

{% hint style="info" %}
Rocky Linux or **AlmaLinux** are now the recommended alternative Enterprise Linux Distro
{% endhint %}

{% hint style="danger" %}
[Significant changes](https://blog.centos.org/2020/12/future-is-centos-stream/) in the future of CentOS have occurred.
{% endhint %}

#### **Reasons for the Change:**

1. **Shift to CentOS Stream:** CentOS Stream has become the rolling-release development version of RHEL, rather than a downstream clone of RHEL. This change means CentOS Stream might receive more frequent updates, which can introduce unpredictability and potential compatibility issues when managing game servers with LinuxGSM.
2. **Impact on Stability:** CentOS Stream's shift towards being an upstream development platform might lead to reduced stability compared to previous CentOS versions. For hosting game servers, a stable environment is crucial to ensure consistent performance and avoid unnecessary disruptions.

| **CentOS version** | Release date | Full updates | Maintenance updates |
| ------------------ | ------------ | ------------ | ------------------- |
| 7                  | 2014-07-07   | 2020-08-06   | 30 June 2024        |
| 8                  | 2019-09-24   | 2021-12-31   |                     |
| Stream 8           | 2019-09-24   | 2024-05-31   |                     |
| Stream 9           | 2021-12-03   | 2027-05-31   |                     |

### Rocky Linux



<figure><img src="../.gitbook/assets/Rocky_Linux.png" alt=""><figcaption></figcaption></figure>

#### **Reasons to use Rocky Linux with LinuxGSM:**

1. **RHEL Compatibility:** Rocky Linux's binary compatibility with RHEL ensures that LinuxGSM, designed to manage game servers on Linux, will run seamlessly on Rocky Linux. This compatibility guarantees a stable environment for hosting game servers and a familiar experience for users transitioning from CentOS.
2. **Stability and Long-Term Support:** Game servers require a stable and reliable operating system to ensure continuous gameplay for players. Rocky Linux's focus on stability and long-term support makes it an ideal choice for hosting game servers with LinuxGSM.
3. **Community-Driven Development:** LinuxGSM benefits from being community-driven, just like Rocky Linux. This alignment in community-focused development fosters a collaborative environment, where users of both projects can actively contribute and seek support from fellow enthusiasts.
4. **Transparent Security Updates:** Regular security updates and patches in Rocky Linux ensure that your game servers remain secure against potential threats. With LinuxGSM's support for automatic updates, maintaining server security becomes a smoother process.

#### **Ideal Use Cases:**

* Game Server Hosting: Rocky Linux's RHEL compatibility and stability make it an excellent choice for deploying and managing game servers with LinuxGSM.
* Continuity from CentOS: For users previously running game servers on CentOS with LinuxGSM, transitioning to Rocky Linux ensures a familiar and stable environment.

### **AlmaLinux**



<figure><img src="../.gitbook/assets/Almalinux-logo-white-v2.png" alt=""><figcaption></figcaption></figure>

#### **Reasons to use AlmaLinux with LinuxGSM:**

1. **RHEL Compatibility:** **AlmaLinux i**s direct binary compatibility with RHEL ensures that LinuxGSM will run seamlessly on **AlmaLinux**, providing a stable platform for hosting game servers.
2. **Community-Driven Development:** LinuxGSM benefits from being community-driven, just like Rocky Linux. This alignment in community-focused development fosters a collaborative environment, where users of both projects can actively contribute and seek support from fellow enthusiasts.
3. **Long-Term Support and Stability:** Game servers require consistent performance and long-term support to avoid disruptions. **AlmaLinux**'s commitment to stability and long-term support aligns with the requirements of managing game servers using LinuxGSM.
4. **Security Emphasis:** **AlmaLinux** prioritizes security, providing timely updates and patches. When combined with LinuxGSM's capabilities for automated updates, you can maintain a secure gaming environment effortlessly.

#### **Ideal Use Cases:**

* CentOS Replacement: For users transitioning from CentOS to **AlmaLinux** for hosting game servers with LinuxGSM, the distribution's RHEL compatibility ensures continuity and stability.
* Enterprise Game Server Deployments: **AlmaLinux**'s enterprise-grade stability and long-term support make it well-suited for hosting game servers in professional gaming environments.

### EPEL

LinuxGSM uses packages that are not available by default in CentOS because of this the EPEL (Extra Packages for Enterprise Linux) repository is required to install all dependencies. EPEL is a repository managed by the Fedora project to add extra packages to RHEL/CentOS.

{% hint style="info" %}
EPEL is required to run LinuxGSM
{% endhint %}
