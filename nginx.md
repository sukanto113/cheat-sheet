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

### Add proxy site

```
server {
    listen 80;
    server_name domain.com;

    location / {
        proxy_set_header x-forwarded-host "domain.com";
        proxy_pass http://localhost:3000;
    }
}
```

### Setup timeout and body size

```
server {
    listen 80;
    server_name domain.com;

    proxy_read_timeout 300;
    proxy_connect_timeout 300;
    proxy_send_timeout 300;
    client_max_body_size 20M;

    location / {
        proxy_set_header x-forwarded-host "domain.com";
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://localhost:3000;
    }
}
```

### Redirect to another location

```
server {
    listen 80;

    server_name domain.com;
    return 301 https://www.domain.com$request_uri;
}
```

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
