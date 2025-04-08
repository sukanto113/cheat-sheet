# install redis
sudo add-apt-repository ppa:redislabs/redis -y
sudo apt update
apt install redis-server -y
systemctl restart redis.service

# setup auth
sudo vim /etc/redis/redis.conf
foobared
```conf
bind 0.0.0.0

protected-mode no

requirepass mypassword
```

systemctl restart redis.service
systemctl status redis-server.service