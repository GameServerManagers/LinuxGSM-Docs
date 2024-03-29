---
description: Make apache2 webserver case insensitive with apache2 mod_speling
---

# Make Webserver Case Insensitive

Some games require FastDL to be case insensitive, apache2 is case sensitive by default. Enabling apache2 mod\_speling ignores case sensitivity on a LAMP stack. This guide applies to debian and ubuntu. At the bottom of this page are external guides that include CentOS/Fedora. **This workaround will not work on shared webhosting** **where editing apache2 files is not available.**

&#x20;Enable mod\_speling:

```
a2enmod speling
```

&#x20;Restart apache:

```
service apache2 restart
```

Apache needs to be told which directories mod\_speling is applied to, open the webserver's .conf file located inside /etc/apache2/sites-available/ and set AllowOverride to All.

 Example:

```
<Directory /var/www/html/>
	Options Indexes FollowSymLinks
	AllowOverride All
	Require all granted
</Directory>
```

Set apache2 to use the .conf file you just edited:

```
a2ensite name_of_.conf_file
```

 In /var/www/html/ or your webserver directory, create a .htaccess file with this:

```
<IfModule mod_speling.c>
CheckSpelling On
CheckCaseOnly On
</IfModule>
```

 Test the configuration by creating a file, like test.txt, and see if it can be opened in browser by typing TEST.txt, test.TXT, etc. If it works, you are finished.



[mod\_speling Documentation](https://httpd.apache.org/docs/2.4/mod/mod\_speling.html)

Guides from other sources:

[Wikitechy mod\_speling Guide](https://www.wikitechy.com/tutorials/apache/how-to-use-the-mod-speling-apache-module)

[a2Hosting mod\_speling Guide](https://www.a2hosting.com/kb/developer-corner/apache-web-server/using-the-mod-speling-apache-module)

&#x20;

 
