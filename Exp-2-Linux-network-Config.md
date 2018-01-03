# Expriment No : 2 Linux Network Configuration 
                                                 Created By: Saurabh Patil
                                                              9773445201

##### To-do- List: 
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

 To configure a network connection with the Network Administration Tool, perform the following steps:

   * Add a network device associated with the physical hardware device.
    * Add the physical hardware device to the hardware list, if it does not already exist.
    * Configure the hostname and DNS settings.
    * Configure any hosts that cannot be looked up through DNS. 




##### DNS (Domain Name System or Service) 

It a hierarchical decentralized naming system/service that translates domain names into IP addresses on the Internet or a private network and a server that provides such a service is called a DNS server.

Lets learn , how to setup a local DNS using the hosts file (/etc/hosts) in Linux systems for local domain resolution or testing the website before taking live.

For example, you may want to test a website locally with a custom domain name before going live publicly by modifying the /etc/hosts file on your local system to point the domain name to the IP address of the local DNS server you configured.

The /etc/hosts is an operating system file that translate hostnames or domain names to IP addresses. This is useful for testing websites changes or the SSL setup before taking a website publicly live.

` IMP-NOTE `: This method will only work if the hosts have a static IP address. Therefore ensure that you have set static IP addresses for your Linux hosts or nodes running other operating systems.

#### Configure DNS Locally Using /etc/hosts File in Linux

Now open the /etc/hosts file using your editor of choice as follows
```
$ sudo vi /etc/hosts // or
$ sudo gedit /etc/hosts
```
Then add the lines below to the end of the file as shown in the screen shot below.
```
192.168.56.1   ubuntu.tecmint.lan
192.168.56.10  centos.tecmint.lan
```
Next, test if everything is working well as expected, using the ping command from Host 1, you can ping Host 2 using it domain name like so.
```
$ ping -c 4 centos.tecmint.lan 
OR
$ ping -c 4 centos
```

