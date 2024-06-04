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

## Refference:

- [How to Install and Configure SSH on Ubuntu 22.04](https://hostman.com/tutorials/how-to-install-and-configure-ssh-on-ubuntu-22-04/)
