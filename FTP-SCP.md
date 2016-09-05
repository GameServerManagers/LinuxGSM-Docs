# SFTP

SFTP is the transfer protocol included with SSH. Unlike FTP, it benefits from encryption.  
We can only advise to use SFTP.  
scp is the corresponding command that you can use to transfer files over SSH.

Note : A good practice, is to use a secured encryption key. Otherwise, it'd be theorically possible sniff your network and decode your traffic.

#### Advantages

* Encrypted: less chances for your data to get stolen
* Nothing to install
* Works like any other than FTP server
* Compatible with the popular Filezilla  
* You can login to users out of the box

#### How to use SFTP 

* Connect like any FTP except it's on your SSH port (default 22)
* Use your username / password
* You might need to set protocol to SFTP in your FTP client.


# Bad practice to avoid

## By all means, you should never 

1. Connect to an FTP server as root unless there is a very good reason and you know what you're doing.
2. Use FTP anymore. Prefer SFTP.

### Root login to an FTP

Here is why you shouldn't

* By logging in as root, you might accidentally remove essential system files or put useless files into the wrong place and mess up with your system.
* But even more annoying, any file you'll write will belong to root, and the user won't be able to either read, change, or execute writtent files as root.
* FTP is an unencrypted protocol, therefore it is very unsecured to edit sensitive files using it.

#### How to operate without root FTP login ?

* If you need to edit system config files, then do like everyone else : use an SSH text editor like "nano" or "vi". 
* Set your FTP so that you can login as users with a valid shell from the machine. Eventually, disable root FTP login.
* Oh, one more thing... Don't use FTP, use SFTP, at the very least.