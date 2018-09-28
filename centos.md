# Centos tips

## Configure DNS suffixes search

### edit resolv.conf
[plenoir@1lxplenoir-pad ~]$ sudo vi /etc/resolv.conf
### add the list of suffixes
search oad.exch.int europe.nyx.com prod.exch.int devqa.exch.int eua.exch.int oad.exch.int devqa.exch.int eua.exch.int prod.exch.int
### edit the NetworkManager configuration to prevent NM to overwrite changes
[plenoir@1lxplenoir-pad ~]$ sudo vi /etc/NetworkManager/NetworkManager.conf
### tell NetworkManager to not modify the DNS settings
[main]

dns=none
### restart NM first, then network
[plenoir@1lxplenoir-pad ~]$ sudo systemctl restart NetworkManager
[plenoir@1lxplenoir-pad ~]$ sudo systemctl restart network.service
### now test
[plenoir@1lxplenoir-pad ~]$ host qpdpekfk24101-int
qpdpekfk24101-int.devqa.exch.int has address 172.26.160.14


## docker

### install Docker
https://docs.docker.com/install/linux/docker-ce/centos/#install-docker-ce

### Configure Docker to start on boot

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use systemd to manage which services start when the system boots.

$ sudo systemctl enable docker

To disable this behavior, use disable instead.

$ sudo systemctl disable docker


### Docker behind a proxy
https://stackoverflow.com/questions/23111631/cannot-download-docker-images-behind-a-proxy

### Fix permission issue
https://stackoverflow.com/questions/44065827/jenkins-wrong-volume-permissions
