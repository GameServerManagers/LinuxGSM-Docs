# server-migration

It is possible to migrate an exising game server to LinuxGSM.

1. Install the LinuxGSM server of choice as normal.
2. Once installed there will be a vanilla install in `servervfiles`
3. Backup the serverfiles mv`serverfiles serverfilesbak`
4. create a new serverfiles directory `mkdir serverfiles`
5. Copy your existing server in to the empty serverfiles directory.
6. Ensure that the file stucture matches that of `serverfilesbak` i.e the executable,maps etc. are in the same place.
7. Ensure the correct user permissions are used `chown -r gameserver:gameserver serverfiles`
8. Copy the game server config to the new config file location found in `./gameserver details`
9. Run update to make sure you are up-to-date `./gameserver update`
10. Test that the server works.
11. Once complete delete `serverfilesbak`
