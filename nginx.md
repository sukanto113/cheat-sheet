# Nginx cheat sheet

## Install nginx

```
$ sudo apt update && sudo apt upgrade -y
$ sudo apt install nginx -y
$ sudo systemctl status nginx
```

### Run nginx if not running

```
$ sudo systemctl start nginx
```

### Restart nginx service

```
$ sudo systemctl restart nginx
```

### Test config syntax

```
$ nginx -t
```

### Apply config changes

```
$ nginx -s reload
```

## Add site

### Add static site

1. Create file `/etc/nginx/sites-available/domain.com`
2. Put the content

```
server {
listen 80;
server_name domain.com;

    root /srv/static/domain.com;

}
```

3. Link `domain.com` to `sites-enabled`.

```
$ ln -s /etc/nginx/sites-available/domain.com /etc/nginx/sites-enabled/domain.com
```

4. Put a `index.html` file in `/srv/static/domain.com` directory

5. Test and apply config changes.

## Setup SSL certificate

### Install cartbot

```
$ sudo snap install --classic certbot
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

### Get cerficicate

```
$ sudo certbot --nginx
```
