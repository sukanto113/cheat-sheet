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
    client_max_body_size 500M;

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

### Serve static website

```
server {
    listen 80;
    server_name your-domain.com; # or IP if no domain

    root /var/www/my-vite-app;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## fix 522 error

### Increase the SYN backlog

$ sudo nano /etc/sysctl.conf

```
net.ipv4.tcp_max_syn_backlog=8192
net.core.somaxconn=8192
```

$ sudo sysctl -p

### Raise nginx capacity (the core fix)

$ vim /etc/nginx/nginx.conf

```
worker_processes auto;
worker_rlimit_nofile 65535;

events {
    worker_connections 8192;
    multi_accept on;
}

http {
    ...
    keepalive_timeout 90;
    ...
}
```

$ vim /etc/nginx/sites-enabled/default

```
listen 80 default_server backlog=4096;
```

$ vim app.betterenrich.com

```
listen 443 ssl backlog=4096; # managed by Certbot
```

Then apply with a full restart

```sh
nginx -t && sudo systemctl restart nginx
ss -ltn 'sport = :443'    # Send-Q should now show 4096, not 511
```

### Stop burning a connection per request to Next.js

this is not a required fix for 522 it is supporting a fix.

$ vim /etc/nginx/sites-available/app.betterenrich.com

```

upstream betterenrich_app {
server 127.0.0.1:3001;
keepalive 64;
}

server {
...
location / {
 proxy_pass http://betterenrich_app;

        # These two lines enable connection reuse to the app
        proxy_http_version 1.1;
        proxy_set_header Connection "";

        # Headers
        proxy_set_header Host $host;
        proxy_set_header x-forwarded-host "app.betterenrich.com";
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
    }

}

```

### Check error count

watch -d 'netstat -s | grep -i listen' # counters should stop climbing
ss -ltn # Recv-Q should stay near 0 on LISTEN sockets

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
