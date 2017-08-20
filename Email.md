<p align="center"><img src="http://i.imgur.com/kP4Doap.png" alt="Email icon" width="200"/></p>
<p align="center">Send LinuxGSM alerts to an email addresses.</p>
<p align="center"><img src="https://gameservermanagers.com/wp-content/uploads/2016/01/lgsm-monitor.png" alt="Email Alert"/></p>

# Sending emails
LinuxGSM will attempt to send an email using the `mail` command. 

Postfix or equivalent must be setup and correctly configured before sending emails. Failure to correctly configure Postfix and a domain for your server will mean that the email alert may be flagged as spam or not arrive at all. Configuring postfix is not covered here but there are many tutorials online to help.

# Enable Email alerts
To enable email alerts you will need to add an email address to the LinuxGSM config.

````bash
# Email Alerts | https://github.com/GameServerManagers/LinuxGSM/wiki/Email
emailalert="off"
email="email@example.com"
emailfrom=""
````
#

# Send Test Alert
Finally test that is correctly works by sending a test alert.
```
./gameserver test-alert
```
