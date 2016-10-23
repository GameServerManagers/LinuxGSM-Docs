## Alerts

Alerts allow you to receive an email if the server is monitored down, restarted or updated (See [[Monitor]]). That notification will include some of the logs to help you diagnose what caused the crash. Make sure that you installed mailx (mailutils) and postfix or any other mail server that can send mails.

To enable them, edit your script accordingly : 

#### Email:
````bash
emailalert="on"
email="email@example.com" # Destination email
emailfrom="" # Sender email, useful if you have an FQDN with proper email settings
````
