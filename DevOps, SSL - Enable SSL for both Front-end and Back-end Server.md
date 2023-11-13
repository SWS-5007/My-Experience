# DevOps, SSL - Enable SSL for both Front-end and Back-end Server

I installed the SSL on Server but one Error occurred when I call from Front-end (:3000 port) to Back-end (:5000 port).

>POST https://52.0.209.15/api/login net::ERR_CERT_COMMON_NAME_INVALID

This means SSL wasn't not enabled for both Front-end and Back-end Server (Two subdomains) successfully.

So I updated the SSL VirtualHost in /etc/apache2/sites-enabled/default-ssl.conf like below.


`cd /etc/apache2/sites-enabled/default-ssl.conf`

```
<VirtualHost *:443>
    ServerName tellmewhentogo.com

    ProxyPreserveHost On

    ProxyPass /api  http://127.0.0.1:5000/
    ProxyPassReverse /api  http://127.0.0.1:5000/

    ProxyPass / http://127.0.0.1:3000/

    ProxyPassReverse / http://127.0.0.1:3000/

    SSLEngine on
    SSLCertificateFile /etc/certificate/ssl.crt
    SSLCertificateKeyFile /etc/certificate/ssl.key
    SSLCertificateChainFile /etc/certificate/ssl.ca-bundle
</VirtualHost>

```

After that, I restarted the apache2 server again.

`sudo a2enconf ssl-params`

`sudo a2ensite default-ssl`

`sudo apache2ctl configtest`

`sudo systemctl restart apache2`
