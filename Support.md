# GitHub issues are for LinuxGSM Development only!
* *YES PLEASE:* Submit any bug, feature suggestion or code contribution to Github.
* *NO THANK YOU:* Game server issues (e.g CS:GO, TF2), Dedicated server issues (e.g Ubuntu, CentOS) or anything not directly related to LinuxGSM development. There are various volunteers that may be able to help with these on the Steam group.

Any issue that is suddenly closed by moderators has been deemed not suitable for the GitHub issues page. Please post elsewhere. If in doubt contact us on discord or post on the steam group.

Don't worry its not that we don't like you, we just need to keep the issues page relevant to LinuxGSM code to assist with our workflow.

# Getting support
We want to help out server admins as best as we can however, our time is limited and is best spent on developing LinuxGSM. Patience is also wearing thin on unhelpful posts. So please help us by providing the following information when posting to help us to resolve YOUR issue.

## Search Before Asking

## Official Documentation
The LinuxGSM website and Wiki will tell you almost anything you need about LinuxGSM.

- https://linuxgsm.com  
- https://linuxgsm.com/wiki

## Google
It is likely that somebody already asked your question before. Save time for yourself and everyone else using Google first.

> “Google is how I learnt and still learn to use BASH and develop LinuxGSM.” - Daniel Gibbs

- https://google.com

## Updates

Make sure your LinuxGSM script is up to date.

`./gameserver update-lgsm`

# Required Information for Support
Some details are required to help us solve your problem. If you refuse to provide this information we are unable to help you.

## Minimum information - _to get help_

- Which **game server** you are running (e.g Rust/CS:GO).
- The **outputted link** of `./gameserver postdetails` command.
- The context of your error and the exact outputs.

If for some reason, you cannot use postdetails, then provide:
- Your Linux **distro** and **version** (e.g Ubuntu 16.04 x64).
- Your **kernel** information ( `uname -a` )
- Your versions for **glibc** ( `ldd --version` ) and **tmux** ( `tmux -V` )

## Additional information - _that is usually useful_

- Any useful **log** in `/home/gameserver/log` (use pastebin or equivalent).
- Any useful **screenshots**.
- Your basic **server hardware** (CPU/RAM/Storage/Bandwidth).
- Any **test** you have already tried.
- Any **relevant information** you think will help.

# Support Links

## General Support

- **Discord** https://linuxgsm.com/discord

- **Steam group** https://linuxgsm.com/steam

# GitHub Labels Proposal
Im am proposing an improvement to the labelling system on GitHub to better allow devs and end users to get good feedback on the status of an issue. I would also like to investigate any github issues bots (discord bots are great) allowing auto messaging to common problems like lack of info or being posted in the wrong forum. Auto label bot would also be useful.

Labels are to be split in to several category's

* Distro/Game/Platform: Details about what the issue relates to.
* Outcome: When an issue is closed what was the outcome.
* Status: What is currently happening to the issue.
* Type: What type of issue it is.
* Priority: Only the urgent issues.
