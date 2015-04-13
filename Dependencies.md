Below is a complete list of dependencies required for all servers. Use your distros package manager (apt-get, yum etc) to install these requirements.

These should be installed before installing any LGSM server.

## Notes
### Distro Compatibility
The older the server the less likely the game server will work on your server. For example CentOS 5 does not work with most servers. However CentOS 6 can but may require glibc fixes.

### Recommended Distros
The below servers are the most compatible and work well with all servers.

* => Ubuntu 12.04 LTS
* CentOS 7

However any distro with _=> GLIBC 2.15_ and _=> tmux 1.6_ will also be compatible with all servers.
### CentOS 6 EPEL
LGSM requires you install [EPEL](http://download.fedoraproject.org/pub/epel/6/i386/repoview/epel-release.html) if running CentOS 6.

This is because tmux is not available as a standard package in CentOS 6.
### Ubuntu Releases
Only LTS releases are listed here as the dependencies don't normally change between LTS releases. However if a difference is found a non LTS release will be added until the newer LTS release is available.