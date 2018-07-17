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

ppdmoifd07901.prod.exch.int
ppdmoifd07902.prod.exch.int
ppdmoifd07903.prod.exch.int
ppdmoifd07904.prod.exch.int
