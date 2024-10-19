https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/

```
$ sudo apt-get install gnupg curl
$ curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor
$ echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
$ sudo apt-get update
$ sudo apt-get install -y mongodb-org
$ sudo systemctl start mongod
$ sudo systemctl daemon-reload
$ sudo systemctl status mongod
$ sudo systemctl enable mongod

```

https://www.hostinger.com/tutorials/how-to-install-mongodb-on-ubuntu/

```
$ vim /etc/mongod.conf
$ sudo systemctl restart mongod
$ mongosh
$ netstat -tuln
$ telnet 185.164.111.37 27017
```

```
$ ls -lrt /tmp/mongodb-27017.sock
```