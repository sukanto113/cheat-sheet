### Install PHP

```
$ sudo apt install php-cli php-fpm php-mysql php-json php-opcache php-mbstring php-xml php-gd php-curl
```

### Install WordPress with Nginx

```
$ mkdir -p /var/www/html/sample.com
$ cd /tmp
$ wget https://wordpress.org/latest.tar.gz
$ tar xf latest.tar.gz
$ sudo mv /tmp/wordpress/* /var/www/html/sample.com/
$ sudo chown -R www-data: /var/www/html/sample.com
```

### Configure Nginx for WordPress


```
server {
    listen 80;
    server_name sample.com;

    root /var/www/html/sample.com;
    index index.php;

    # log files
    access_log /var/log/nginx/sample.com.access.log;
    error_log /var/log/nginx/sample.com.error.log;

    location = /favicon.ico {
        log_not_found off;
        access_log off;
    }

    location = /robots.txt {
        allow all;
        log_not_found off;
        access_log off;
    }

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php-fpm.sock;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires max;
        log_not_found off;
    }
}
```

```
$ sudo ln -s /etc/nginx/sites-available/sample.com /etc/nginx/sites-enabled/
```

## Refference:

- [WordPress Nginx: Everything You Need to Know About Installing WordPress on Ubuntu](https://www.hostinger.com/tutorials/how-to-install-wordpress-with-nginx-on-ubuntu/)
