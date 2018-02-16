You can migrate an exising server to LinuxGSM. You can also migrate an oldly installed server to a freshly LinuxGSM installed server.

* Install your LinuxGSM blank server
* Edit its LinuxGSM configuration; see [[LinuxGSM-Config]]
* Copy any relevant content in your server's data files. The LinuxGSM server files directory is `serverfiles`. Do not forget to apply proper files ownership if copying data using root; see [[File-Ownership]]
* If applicable, rename your config files with the proper names (example: csgoserver.cfg); see [[Game-Server-Config]] for more information about how LinuxGSM handles config files.