Working with Kali Linux

## Change MAC address
First, run the terminal as ROOT:
```
kali@kali:~$ sudo -i
```
Then:
```
root@kali:~# ifconfig
root@kali:~# ifconfig eth0 down
root@kali:~# ifconfig eth0 hw ether 00:11:22:33:44:55
root@kali:~# ifconfig eth0 up
root@kali:~# ifconfig 
```


To get original MAC address:
```
ethtool -P eth0
```
