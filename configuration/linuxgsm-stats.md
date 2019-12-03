# LinuxGSM Stats

LinuxGSM Stats is an `opt in` voluntary feature that allows you to provide selected information about your game server to the lead developer of LinuxGSM \(Daniel Gibbs\) by enabling the `stats` setting.

## How is the information used?

All data collected is used to provide an insight of which game servers, distro and servers are popular with game server admins. This will assist in prioritising LinuxGSM development and give me \(Daniel Gibbs\) a never before insight of the numbers of people using LinuxGSM. This is a massive personal motivator as it has previously been difficult to know how many people actually use LinuxGSM.

## What information is collected?

Below is a list of types of data collected

### Basic Info

* Game Server - Knowing the game server you are running gives insights in to which servers are popular and can help shape development priorities.
* Distro - It is useful to know which distros LinuxGSM is being used on to help focus development.
* LinuxGSM Version - The currently installed version of LInuxGSM.

### Game Server Usage

Gathering game server usage helps set the minimum required hardware for each game server. This is particularly useful for resource intensive servers.

* CPU Used - The CPU usage  in MHz \(rounded to the neared 100MHz\) of the game server.
* RAM Used - The memory usage in MB \(rounded to the neared 100MB\) of the game server.
* Disk Used - This storage taken by the game server \(serverfiles directory\) of the game server.

### Server Hardware

Gathering information on the server hardware being used to host a Game Server. This provides useful stats on the sorts of hardware game server admins are deciding to use.

* CPU - Gathers the CPU Manufacturer and Model.
* RAM - Total server RAM.
* Disk Space - Total server disk space.

### Country of origin

The country of origin is show identifying where in the world LinuxGSM is being used.

## How is Information collected?

LinuxGSM Stats uses Google Analytics to collect information to allow Daniel Gibbs to get an idea of which game servers and distros are popular identify system requirements for game servers and know the sort of servers game server admins are using.

## Is my data anonymous?

Short answer - Yes

Long answer - All information gathered is anonymous, the server IP address, hostname etc or other identifying information is not collected.   
  
When LinuxGSM Stats is first run it creates a [UUID \(Unique identifier\)](https://en.wikipedia.org/wiki/Universally_unique_identifier) which is a randomly generated ID to allow Google Analytics to identify your unique information anonymously. Since this ID is random there is no way to know where the info is from, only that it is from the same sender. 

The UUID is located in`lgsm/data/uuid.txt`,if this file is deleted a new UUID will be generated.

## How frequently is the data sent?

Data is sent every time the monitor runs as this is the only way send regularly send data.

## How can i enable this feature?

To enable LinuxGSM Stats simply add the `stats="on"` setting to the `common.cfg` file. This can also be enabled on install.





