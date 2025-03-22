# SSH cheat sheet

## Install open-ssh server

```
$ sudo apt update && sudo apt upgrade
$ sudo apt install openssh-server
$ sudo systemctl enable --now ssh
$ sudo systemctl status ssh
```

## Commands

### Copy a file from remote to local

```
$ scp username@remoteHost:/remote/dir/file.txt /local/dir/
```

### Copy a file from local to remote

```
$ scp /local/dir/file.txt username@remoteHost:/remote/dir/
```

## setup local ssh key to vps for login
```sh
$ cat ~/.ssh/id_rsa.pub | ssh user@your-vps-ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

$ ssh user@your-vps-ip
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys
```

## Refference:

- [How to Install and Configure SSH on Ubuntu 22.04](https://hostman.com/tutorials/how-to-install-and-configure-ssh-on-ubuntu-22-04/)
