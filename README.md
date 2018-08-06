# README

## access
+ Static IP: `18.185.209.54`
+ DNS name using no-ip: `udacity-aws.ddns.net`
+ Startpage URL: `http://udacity-aws.ddns.net`

## installed software
+ apache2
+ python3
+ python3-pip
+ postgresql
+ libapache2-mod-wsgi-py3
+ git
+ current updates

## configuration

#### firewall (ufw and lightsail)
+ Outgoing: all allowed
+ Incoming: SSH, NTP and HTTP only

#### SSH
+ port: changed as required: `Port xxxx`
+ No remote login using root: `PermitRootLogin no`
+ No password authentication: `PasswordAuthentication no`
+ Public key authentication only
+ Only `grader` and `ubuntu` allowed to log in remotely: `AllowUsers ubuntu grader`


#### apache
+ using mod_wsgi to serve flask app:
+ app located in `/var/www/html/udacity-backend/project`
+ Enabled `rewrite` and `headers` modules for following security settings
+ Some additional apache security hardening settings:
```
ServerName udacity-aws
ServerTokens Prod
ServerSignature Off
FileETag None
TraceEnable off
Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure
Header always append X-Frame-Options SAMEORIGIN
Header set X-XSS-Protection 1;mode=block
RewriteEngine On RewriteCond %{THE_REQUEST} !HTTP/1.1$
RewriteRule .* - [F]
Timeout 60
```

#### postgresql
+ no remote connections
+ created user `catalog`
+ `catalog` given permission to update, select, insert, delete on tables used by
  the application only:
  ```
  REVOKE ALL ON table_name FROM catalog;
  GRANT UPDATE, SELECT, INSERT, DELETE ON table_name TO catalog;
  ```

## resources
+ apache documentation: `https://httpd.apache.org/docs/2.4/`
+ flask dosumentation: `http://flask.pocoo.org/docs/1.0/`
+ postgresql documentation: `https://www.postgresql.org/docs/9.5/static/index.html`
+ SQLAlchemy documentation: `http://docs.sqlalchemy.org/en/latest/`
+ Dynamic DNS: `https://www.noip.com`
+ Stackoverflow (various topics): `https://stackoverflow.com`
