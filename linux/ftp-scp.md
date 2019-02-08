# ftp-scp

SFTP \(SSH File Transfer Protocol\) is the transfer protocol to view and transfer files over SSH. SFTP works the same as FTP but it is encrypted.

## SFTP Advantages

* Encrypted
* Nothing extra to install \(such as FTP server\)
* Works like any other FTP server
* Compatible with the popular clients such as Filezilla and WinSCP
* You can login to any SSH accessable Linux user.

## How to use SFTP

* Connect like any FTP except it uses the port \(default 22\)
* Use your linux username / password
* You might need to set protocol to SFTP in your FTP client.

## Bad practice to avoid

### By all means, you should **never**

1. Connect to a server as root.
2. Use FTP if SFTP is available.

#### Root login to an FTP

Here is why you shouldn't

* By logging in as root, you might accidentally remove essential system files or put useless files into the wrong place and mess up with your system.
* But even more annoying, any file you'll write will belong to root, and the user won't be able to either read, change, or execute written files as root.
* FTP is an unencrypted protocol, therefore it is very unsecured to edit sensitive files using it.

**How to operate without root FTP login?**

* If you need to edit system config files, then do like everyone else: use an SSH text editor like `nano` or `vi`.
* Set your FTP so that you can login as users with a valid shell from the machine. Eventually, disable root FTP login.
* Oh, one more thing... Did we talk about SFTP?
