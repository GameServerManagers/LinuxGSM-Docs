Here are the Dont Starve Together install guides. A Linux one is included. There is a step within the guide about Authentication Tokens.
http://steamcommunity.com/id/ToNiO44/myworkshopfiles/?section=guides&appid=322330

# The Below instructions are out of date.
For further info on DST Dedicated servers visit this wiki http://dont-starve-game.wikia.com/wiki/Guides/Don%E2%80%99t_Starve_Together_Dedicated_Servers

# Getting your Authentication Token

1. Start Don't Starve Together from Steam and click on the "Play!" button.

![DST Title](images/dst/DST_title.png)

2. Click on the "Acct Info" button.

![DST Menu](images/dst/DST_menu.png)

3. Click on the "Generate Server Token" button, copy the token, and paste it into the file:

~/.klei/DoNotStarveTogether/MyDediServer/cluster_token.txt 

You can quickly do this by running the following command, replacing YourServerTokenHere with your server token (Keep the quotes around the token).

echo 'YourServerTokenHere' > ~/.klei/DoNotStarveTogether/MyDediServer/cluster_token.txt