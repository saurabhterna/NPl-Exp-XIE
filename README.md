# 1.ifconfig
    # ifconfig

ifconfig (interface configurator) command is use to initialize an interface, assign IP Address to interface and enable or disable interface on demand. With this command you can view IP Address and Hardware or MAC address assign to interface and also MTU (Maximum transmission unit) size.
#### ifconfig eth0
ifconfig with interface (eth0) command only shows specific interface details like IP Address, MAC Address etc. with -a options will display all available interface details if it is disable also.

#### Assigning IP Address and Gateway
    # ifconfig eth0 192.168.50.5 netmask 255.255.255.0
Assigning an IP Address and Gateway to interface on the fly. The setting will be removed in case of system reboot.

##### Enable or Disable Specific Interface
To enable or disable specific Interface, we use example command as follows.
##### Enable eth0
    # ifup eth0
##### Disable eth0
    # ifdown eth0

##### Setting MTU Size
    # ifconfig eth0 mtu XXXX
By default MTU size is 1500. We can set required MTU size with below command. Replace XXXX with size.

##### Set Interface in Promiscuous mode
    # ifconfig eth0 - promisc   
Network interface only received packets belongs to that particular NIC. If you put interface in promiscuous mode it will received all the packets. This is very useful to capture packets and analyze later. For this you may require superuser access.

# 2. PING Command
    # ping 152.25.24.6
    # ping -c 5 www.tecmint.com
PING (Packet INternet Groper) command is the best way to test connectivity between two nodes. Whether it is Local Area Network (LAN) or Wide Area Network (WAN). Ping use ICMP (Internet Control Message Protocol) to communicate to other devices. You can ping host name of ip address using below command.

# 3. TRACEROUTE Command
    # traceroute 152.25.4.55
traceroute is a network troubleshooting utility which shows number of hops taken  to reach destination also determine packets traveling path. Below we are tracing route to global DNS server IP Address and able to reach destination also shows path of that packet is traveling.

# 4. NETSTAT Command
    # netstat -a // Listing all ports (both TCP and UDP) using netstat -a 
    # netstat -at // Listing only TCP (Transmission Control Protocol) 
    # netstat -l // Listing all active listening ports connections
    # netstat -r // Display Kernel IP routing table with netstat
    
Netstat (Network Statistic) command display connection info, routing table information etc. To displays routing table information use option as -r.




