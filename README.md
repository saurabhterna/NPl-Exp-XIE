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

# 5. DIG Command
    # dig www.tecmint.com
Dig (domain information groper) query DNS related information like A Record, CNAME, MX Record etc. This command mainly use to troubleshoot DNS related query.

Dig command reads the /etc/resolv.conf file and querying the DNS servers listed there. The response from the DNS server is what dig displays.
###### Let us understand the output of the commands:
Lines beginning with ; are comments not part of the information.
* The first line tell us the version of dig (9.8.2) command.
* Next, dig shows the header of the response it received from the DNS server
* Next comes the question section, which simply tells us the query, which in this case is a query for the “A” record of yahoo.com. The IN means this is an Internet lookup (in the Internet class).
* The answer section tells us that yahoo.com has the IP address 72.30.38.140
* Lastly there are some stats about the query. You can turn off these stats using the +nostats option.

# 6. NSLOOKUP Command
    # nslookup www.xavierengg.com
nslookup command also use to find out DNS related query. The following examples shows A Record (IP Address) of xavierengg.com.

# 7. ROUTE Command
    # route
    # route add -net 10.10.10.0/24 gw 192.168.0.1 // add route
    # route del -net 10.10.10.0/24 gw 192.168.0.1 // delete route
    # route add default gw 192.168.0.1 // add default Gateway
    
route command also shows and manipulate ip routing table. To see default routing table in Linux, type the following command.










