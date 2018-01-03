# Expriment No :3  Multiple IP Addresses to Network Interface
                                                 Created By: Saurabh Patil
                                                              9773445201
To-Do List: 
- Create Multiple IP Addresses to One Single Network Interface

The concept of creating or configuring multiple IP addresses on a single network interface is called ` IP aliasing `. IP aliasing is very useful for setting up multiple virtual sites on Apache using one single network interface with different IP addresses on a single subnet network.

- The main advantage of using this IP aliasing is, you don’t need to have a physical adapter attached to each IP, but instead you can create multiple or many virtual interfaces (aliases) to a single physical card.

##### Linux IP Aliasing

Create Multiple IP Addresses in One NiC

I have an interface called “ifcfg-eth0“, the default interface for the Ethernet device. If you’ve attached second Ethernet device, then there would be an “ifcfg-eth1” device and so on for each device you’ve attached. These device network files are located in “/etc/sysconfig/network-scripts/” directory. Navigate to the directory and do “ls -l” to list all devices.
```
# cd /etc/sysconfig/network-scripts/
# ls -l
```
Sample Output
```
ifcfg-eth0   ifdown-isdn    ifup-aliases  ifup-plusb     init.ipv6-global
ifcfg-lo     ifdown-post    ifup-bnep     ifup-post      net.hotplug
ifdown       ifdown-ppp     ifup-eth      ifup-ppp       network-functions
ifdown-bnep  ifdown-routes  ifup-ippp     ifup-routes    network-functions-ipv6
ifdown-eth   ifdown-sit     ifup-ipv6     ifup-sit
ifdown-ippp  ifdown-tunnel  ifup-isdn     ifup-tunnel
ifdown-ipv6  ifup           ifup-plip     ifup-wireless
```
Let’s assume that we want to create three additional virtual interfaces to bind three IP addresses (172.16.16.126, 172.16.16.127, and 172.16.16.128) to the NIC. So, we need to create three additional alias files, while “ifcfg-eth0” keeps the same primary IP address. This is how we moving forward to setup three aliases to bind the following IP addresses.
```
Adapter            IP Address                Type
-------------------------------------------------
eth0              172.16.16.125            Primary
eth0:0            172.16.16.126            Alias 1
eth0:1            172.16.16.127            Alias 2
eth0:2            172.16.16.128            Alias 3
```
Where “:X” is the device (interface) number to create the aliases for interface eth0. For each alias you must assign a number sequentially. For example, we copying existing parameters of interface “ifcfg-eth0” in virtual interfaces called ifcfg-eth0:0, ifcfg-eth0:1 and ifcfg-eth0:2. Go into the network directory and create the files as shown below.
```
# cd /etc/sysconfig/network-scripts/
# cp ifcfg-eth0 ifcfg-eth0:0
# cp ifcfg-eth0 ifcfg-eth0:1
# cp ifcfg-eth0 ifcfg-eth0:2
```
Open a file ` ifcfg-eth0 ` and view the contents.
```
[root@ network-scripts]# vi ifcfg-eth0
DEVICE="eth0"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=172.16.16.125
NETMASK=255.255.255.224
GATEWAY=172.16.16.100
HWADDR=00:0C:29:28:FD:4C
```
Here we only need two parameters (DEVICE and IPADDR). So, open each file with VI editor and rename the DEVICE name to its corresponding alias and change the IPADDR address. For example, open files “ifcfg-eth0:0“, “ifcfg-eth0:1” and “ifcfg-eth0:2” using VI editor and change both the parameters. Finally it will look similar to below.
ifcfg-eth0:0
```
DEVICE="eth0:0"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=172.16.16.126
NETMASK=255.255.255.224
GATEWAY=172.16.16.100
HWADDR=00:0C:29:28:FD:4C
```
ifcfg-eth0:1
```
DEVICE="eth0:1"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=172.16.16.127
NETMASK=255.255.255.224
GATEWAY=172.16.16.100
HWADDR=00:0C:29:28:FD:4C
```
ifcfg-eth0:2
```
DEVICE="eth0:2"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=172.16.16.128
NETMASK=255.255.255.224
GATEWAY=172.16.16.100
HWADDR=00:0C:29:28:FD:4C
```
Once, you’ve made all changes, save all your changes and restart/start the network service for the changes to reflect.
```
[root@ network-scripts]# /etc/init.d/network restart // or
[root@ network-scripts]# service network restart
```
To verify all the aliases (virtual interface) are up and running, you can use “ifconfig” or “ip” command.
```
[root@ network-scripts]# ifconfig
eth0      Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.125  Bcast:172.16.16.100  Mask:255.255.255.224
inet6 addr: fe80::20c:29ff:fe28:fd4c/64 Scope:Link
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:237 errors:0 dropped:0 overruns:0 frame:0
TX packets:198 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:25429 (24.8 KiB)  TX bytes:26910 (26.2 KiB)
Interrupt:18 Base address:0x2000
eth0:0    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.126  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
eth0:1    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.127  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
eth0:2    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.128  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
```
Ping each of them from different machine. If everything setup correctly, you will get a ping response from each of them.
```
ping 172.16.16.126
ping 172.16.16.127
ping 172.16.16.128
```
Sample Output
```
[root@ ~]# ping 172.16.16.126
PING 172.16.16.126 (172.16.16.126) 56(84) bytes of data.
64 bytes from 172.16.16.126: icmp_seq=1 ttl=64 time=1.33 ms
64 bytes from 172.16.16.126: icmp_seq=2 ttl=64 time=0.165 ms
64 bytes from 172.16.16.126: icmp_seq=3 ttl=64 time=0.159 ms
--- 172.16.16.126 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.159/0.552/1.332/0.551 ms
[root@tecmint ~]# ping 172.16.16.127
PING 172.16.16.127 (172.16.16.127) 56(84) bytes of data.
64 bytes from 172.16.16.127: icmp_seq=1 ttl=64 time=1.33 ms
64 bytes from 172.16.16.127: icmp_seq=2 ttl=64 time=0.165 ms
64 bytes from 172.16.16.127: icmp_seq=3 ttl=64 time=0.159 ms
--- 172.16.16.127 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.159/0.552/1.332/0.551 ms
[root@tecmint ~]# ping 172.16.16.128
PING 172.16.16.128 (172.16.16.128) 56(84) bytes of data.
64 bytes from 172.16.16.128: icmp_seq=1 ttl=64 time=1.33 ms
64 bytes from 172.16.16.128: icmp_seq=2 ttl=64 time=0.165 ms
64 bytes from 172.16.16.128: icmp_seq=3 ttl=64 time=0.159 ms
--- 172.16.16.128 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.159/0.552/1.332/0.551 ms
```
Seems everything working smoothly, With these new IPs’ you can setup virtual sites in Apache, FTP accounts and many other things.


TASK 1 :

##### Assign Multiple IP Address Range

If you would like to create a range of Multiple IP Addresses to a particular interface called “ifcfg-eth0“, we use “ifcfg-eth0-range0” and copy the contains of ifcfg-eth0 on it as shown below.
```
[root@ network-scripts]# cd /etc/sysconfig/network-scripts/
[root@ network-scripts]# cp -p ifcfg-eth0 ifcfg-eth0-range0
```
Now open “ifcfg-eth0-range0” file and add “IPADDR_START” and “IPADDR_END” IP address range as shown below.
```
[root@tecmint network-scripts]# vi ifcfg-eth0-range0
#DEVICE="eth0"
#BOOTPROTO=none
#NM_CONTROLLED="yes"
#ONBOOT=yes
TYPE="Ethernet"
IPADDR_START=172.16.16.126
IPADDR_END=172.16.16.130
IPV6INIT=no
#GATEWAY=172.16.16.100
```
Save it and restart/start network service
```
[root@ network-scripts]# service network restart
```
Verify that virtual interfaces are created with IP Address.
```
[root@ network-scripts]# ifconfig
eth0      Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.125  Bcast:172.16.16.100  Mask:255.255.255.224
inet6 addr: fe80::20c:29ff:fe28:fd4c/64 Scope:Link
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:1385 errors:0 dropped:0 overruns:0 frame:0
TX packets:1249 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:127317 (124.3 KiB)  TX bytes:200787 (196.0 KiB)
Interrupt:18 Base address:0x2000
eth0:0     Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.126  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
eth0:1    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.127  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
eth0:2    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.128  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
eth0:3    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.129  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
eth0:4    Link encap:Ethernet  HWaddr 00:0C:29:28:FD:4C
inet addr:172.16.16.130  Bcast:172.16.16.100  Mask:255.255.255.224
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
Interrupt:18 Base address:0x2000
```


