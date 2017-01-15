Previously known as `update-restart`, `force-update` is a command acting just like [[update]] except it will stop your server, start the update process even if no update appears to be available, then start it back.

It's pretty useful if you're restarting your server on a daily basis with [[cronjobs]] for example, you can just check for updates at the same time without having issues with multiple cronjobs running at the same time.


## Commands

`./gameserver force-update`
`./gameserver fu`
