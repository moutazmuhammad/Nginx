# [Let's Encrypt](https://www.digitalocean.com/community/tutorials/an-introduction-to-let-s-encrypt) - SSL certificates

* let's encrypt the let's encrypt service is a relatively new provider of free automated SSL certificates.

*  In order to generate certificates and automate their renewal, we'll use a tool called [Certbot](https://certbot.eff.org/), which will form the basis of this lesson to demonstrate.

* This being as let's encrypt won't issue certificates for IP addresses. So a valid reachable domain is required.

### Install Certbot:
* First navigate to cert but not f dot org. Select the relevant server software, engine X and the corresponding server
* Then follow the commands

### Generate the SSL certificates via the Let's Encrypt:
```sh
certbot certonly -d yourdomain.com
```

> Note you can use [certbot --nginx] command and certbot will know the domain name from nginx.conf if exists

* To see the generated certificates
```sh
ls -l /etc/letsencrypt/live/yourdomain
```

###  Certificate renewal:
* Unlike traditional SSL certificates, that was valid for one or two years at a time. Let's encrypt certificates are valid for 90 days only.

* To renew certificates manually:
```sh
certbot renew
```

* Certificate renewal daily will use a simple cron job
```sh
crontab -e 
```
Add this to the file
```sh
@daily certbot renew 
```