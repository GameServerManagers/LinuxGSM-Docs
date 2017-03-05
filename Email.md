Email alerts allow you to receive an email if the server crashed or was updated (See [[Monitor]]). The email will include some of the logs to help you diagnose what caused the crash.

# Enable Email alerts
To enable email alerts you will need to edit the `gameserver` script.

````bash
emailalert="on"
email="email@example.com" # Destination email
emailfrom="" # Sender email, useful if you have an FQDN with proper email settings
````

You can test the email feature using `test-alert`
````bash
./gameserver test-alert
````
