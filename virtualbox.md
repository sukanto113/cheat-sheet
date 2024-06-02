# Virtual Box cheat sheet

## Get ip address of a machine

Add host only adapter and run the `sudo dhclient`

```
$ sudo apt install isc-dhcp-client
$ sudo dhclient
$ ip a
```

Ref: [VirtualBox host only adapter interface doesn't get an IP address in Oracle Linux 8](https://superuser.com/questions/1721503/virtualbox-host-only-adapter-interface-doesnt-get-an-ip-address-in-oracle-linux)

### Alternative

Ref: [using netplan](https://linuxconfig.org/change-ip-address-on-ubuntu-server)

## Add host name

Edit `/etc/hosts` file

Ref: [How to edit the Ubuntu hosts file and ping a domain name locally](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/How-to-edit-the-Ubnutu-hosts-file-and-ping-a-domain-name-locally)
