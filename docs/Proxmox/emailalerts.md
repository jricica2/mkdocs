# Setting up Email Alerts in Proxmox

<a href="https://technotim.live/posts/proxmox-alerts/" target="_blank">https://technotim.live/posts/proxmox-alerts/</a>

## Install Prerequisites and Configure Postfix

1. Install prerequisites
```bash
apt update
```
```bash
apt install -y libsasl2-modules mailutils
```

2. Set up an App Password on your sender account (Gmail in this case) - <a href="https://myaccount.google.com/apppasswords" target="_blank">https://myaccount.google.com/apppasswords</a>

3. Configure Postfix
```bash
echo "smtp.gmail.com your-email@gmail.com:YourAppPassword" > /etc/postfix/sasl_passwd
```

4. Set/update permissions for the sasl_passwd file
```bash
chmod 600 /etc/postfix/sasl_passwd
```

5. Hash the file
```bash
postmap hash:/etc/postfix/sasl_passwd
```

6. Verify that the hash .db file was created
```bash
cat /etc/postfix/sasl_passwd.db
```

7. Edit the Postfix configuration
```bash
nano /etc/postfix/main.cf
```

8. Add the following lines at the end:
```
# google mail configuration

relayhost = smtp.gmail.com:587
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_security_options =
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/Entrust_Root_Certification_Authority.pem
smtp_tls_session_cache_database = btree:/var/lib/postfix/smtp_tls_session_cache
smtp_tls_session_cache_timeout = 3600s
```
Also comment out the existing `relayhost = ` line

9. Reload Postfix
```bash
postfix reload
```

10. Send a test email using the following command:
```bash
echo "This is a test message sent from postfix on my Proxmox Server" | mail -s "Test Email from Proxmox" your-email@gmail.com
```

## Fix/Change the From: Name from "root"

1. To fix/change the From: name to show as something other than "root", update and install the PCRE pre-requisite
```bash
apt update
```
```bash
apt install postfix-pcre
```

2. Edit the SMTP header checks file
```bash
nano /etc/postfix/smtp_header_checks
```
```bash
/^From:.*/ REPLACE From: pve1-alert <pve1-alert@something.com>
```
The email address doesn't matter because it's going to get overwritten by RicicaHomelabLogs@gmail.com, so only the name will change.

3. Hash the file
```bash
postmap hash:/etc/postfix/smtp_header_checks
```

4. Check the contents of the hashed file
```bash
cat /etc/postfix/smtp_header_checks.db
```

5. Edit the Postfix config file to add the smtp_header_checks parameter
```bash
nano /etc/postfix/main.cf
```

6. Add the smtp_header_checks parameter to the end of the file:
```bash
smtp_header_checks = pcre:/etc/postfix/smtp_header_checks
```

7. Reload Postfix for the changes to take effect
```bash
postfix reload
```

8. Re-use the previous command to verify the changes took effect
```bash
echo "This is a test message sent from postfix on my Proxmox Server" | mail -s "Test Email from Proxmox" your-email@gmail.com
```
