# Expriment No : 2 Linux Network Configuration 
                                                 Created By: Saurabh Patil
                                                              9773445201


* 1. Configuring NIC’s IP Address.
* 2. Determining IP Address and MAC Address using ifconfig command.
* 3. Changing IP address using ifconfig.
* 4. Static IP Address and Configuration by Editing.
* 5. Determining IP Address using DHCP.
* 6. Configuring Hostname in /etc/hosts file

##### Imp:  The primary network configuration files are as follows:
    /etc/hosts
            The main purpose of this file is to resolve host names that cannot be resolved any other way. It can also be used to resolve host names on small networks with no DNS server. Regardless of the type of network the computer is on, this file should contain a line specifying the IP address of the loopback device (127.0.0.1) as localhost.localdomain. 
  
    /etc/resolv.conf
            This file specifies the IP addresses of DNS servers and the search domain. Unless configured to do otherwise, the network initialization scripts populate this file.
    
    /etc/sysconfig/network
             This file specifies routing and host information for all network interfaces. It is used to contain directives which are to have global effect and not to be interface specific.
             
    /etc/sysconfig/network-scripts/ifcfg-interface-name
            For each network interface, there is a corresponding interface configuration script. Each of these files provide information specific to a particular network interface. 

##### How do i Configure Static IP Address Internet Protocol (IPv4)

Open and edit network configuration file for (eth0 or eth1) using your favorite editor. For example, to assigning IP Address to eth0 interface as follows.
```
[root@ ~]# vi /etc/sysconfig/network-scripts/ifcfg-eth0 // or
[root@ ~]# nano /etc/sysconfig/network-scripts/ifcfg-eth0 // or
[root@ ~]# gedit /etc/sysconfig/network-scripts/ifcfg-eth0
```
Sample output:
```
DEVICE="eth0"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=192.168.50.2
NAME="System eth0"
HWADDR=00:0C:29:28:FD:4C
GATEWAY=192.168.50.1
```

Next, restart network services after entering all the details using the following command.

```
[root@ ~]# service network restart
```
For DHCP Configuration update  ` ifcgf-eth0 ` file, by setting paratmeter to ` BOOTPROTO=dhcp `

Sample output:
```
DEVICE="eth0"
BOOTPROTO=dhcp
ONBOOT=yes
TYPE="Ethernet"
```

Again ` restart network service. ` Always ensure service is restarted to get update made in file.

## Network Configuration uding GUI. 
To use the Network Administration Tool, you must have root privileges. To start the application, go to the Applications (the main menu on the panel) => System Settings => Network, or type the command system-config-network at a shell prompt.

![](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/System_Administration_Guide/images/neat.png)
