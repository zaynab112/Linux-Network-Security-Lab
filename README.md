# Linux-Network-Security-Lab
A practical lab demonstrating Linux administration, Networking, Service discovery and Security hardening.

The objective of this project is to build a Linux environment and demonstrate Linux administration, networking, discovering services and improve security.

## Creating Linux VM

I chose to use Ubuntu server as the operating system because it is a lightweight terminal that will allow me to develop my linux and networking fundamentals.

### Configurations
Virtualisation - I chose virtualisation because I downloaded the arm 64 version as my mac processor is arm based. This allows Ubuntu to run using my macs processor rather than having to copy and act as a different processor.

Ram - I gave the ubuntu server 2GB RAM because it is lightweight so doesn't require as much memory. This was enougn memory to practice linux commands and networking tasks.

Storage - I gave the VM 30GB storage to have enough for the software, files and the server.

### Issues
When installing Ubuntu I had two issues:
- The installation of Ubuntu kept failing as I did not create a virtual hard drive for it to install to. This meant that the system could'nt detect a disk to install Ubuntu so it kept failing. To resolve this I created the virtual drive.
- Once installed the system kept going to the 'try or install Ubuntu' page. This was because the installer file was still in the system so it kept loading up that file. To resolve this I removed the installer file and kept the virtual disk meaning when the system was starting it started the system correctly. 

### VM details
- Hostname: linuxlab
- ip address: 192.168.64.2
- Network Interface: enp0s1
- Default Gateway: 192.168.64.1

### Identifying IP addresses, Services and Ports
### IP address and Default Gateway
<img width="839" height="319" alt="Screenshot 2026-09-09 at 13 02 17" src="https://github.com/user-attachments/assets/35ed0943-ec66-4c2c-870b-542a512fc19e" />

This shows the result of ip addr. The output shows 2 interfaces which is the loopback address and the virtual machines network interface. The output shows the virtual machine's IPv4 address which is 192.168.64.2 and the IPv6 addresses. The output also shows the netwrok interface name which is enp0s1 and the broadcast addresss.

<img width="665" height="100" alt="Screenshot 2026-09-09 at 13 16 47" src="https://github.com/user-attachments/assets/0505fe19-97c4-47d0-8781-545770cf4d6e" />

This shows the result of the command ip route which shows the ubuntu server's routing table. This output shows the VMs default gateway and it also shows the local network. The screenshot also shows the result of the command ip route show default. This command only returns the default gateway for the VM.
### Services and Ports
<img width="802" height="334" alt="Screenshot 2026-09-10 at 16 04 05" src="https://github.com/user-attachments/assets/75fd90e1-9850-46e2-9f23-4c40a37c8c8f" />

This shows the output of the command systemctl using the state flag which filters the results for only the services that are currently running on the system. Without the state flag the output would include all the services on the system even if they're not running. The output shows the name of the service, the state of the service and a description of what the service does.

<img width="1194" height="205" alt="Screenshot 2026-09-10 at 16 17 13" src="https://github.com/user-attachments/assets/3222ff26-be1d-4cef-8061-56360e4331ed" />
This shows the output of the command ss with the options -t, -u, -l, -n. The options filter for the listening ports that are either TCP or UDP ports. The output shows the type of ports, the state of the ports and the port numbers. The output also shows how many packets have been recievd and how many packets are in queue to be sent. In this case no packets have been received by either the TCP or UDP ports and only the TCP ports have packets in queue to be sent. It also shows that DNS uses both TCP and UDP ports.

### Commands Used
- sudo apt update - checks for updates
- hostname - returns the name of the machine
- ip addr - returns all the network interfaces and their ip addresses
- ip route - returns the routing table
- ip route show default - only returns the VMs default gateway
- systemctl list-units --type=service --state=running - returns a list of all the running services
- ss -tuln - returns all the ports that are listening using TCP or UDP

## Nmap Scanning
### Connectivity Testing
<img width="483" height="361" alt="Screenshot 2026-09-15 at 16 27 12" src="https://github.com/user-attachments/assets/6a55b460-7b28-4983-a501-4363f871ed11" />
This shows the result of the command ping. Ping is used to test if a computer can communicate with a another computer by sending packets to the computer. This result shows that there 19 packets were sent from my mac and 19 packets were received by the VM. This means that my mac can communicate with the VM.

### Nmap Scan 
<img width="672" height="174" alt="Screenshot 2026-09-15 at 17 32 23" src="https://github.com/user-attachments/assets/cabd85db-3760-4c02-86a4-e5d88f45acfc" />

This shows the result of the nmap scan using the -sV option. This scan is used to scan the 1000 common ports that are used and using the -sV option means it will try to find the version of the service that is running. The results shows that there was 1 TCP port open which was port 22. It also shows that SSH is running on that port. The scan also listened in on the port to find the version of SSH that was running and found that the port was running openSSH 10.2p1 ubuntu 2ubuntu3.6 of SSH. The scan also identified the operating system used by the VM which was Linux. The scan also shows that there were 999 ports that was closed because there was nothing running on the ports.

<img width="642" height="370" alt="Screenshot 2026-09-16 at 16 22 13" src="https://github.com/user-attachments/assets/b69060cd-77b0-445b-a5e8-eb7d255bab0f" />

This shows the result of the nmap scan using the -p- option. The -p- option is used to scan all 65535 ports. I used this incase there was other ports outside of the 1000 ports that was already scanned. The results shows that even after scanning all the other ports there was only 1 TCP port open. The results of the nmap scan using the -p option is the same result as the nmap scan without the -p option.

### Commands Used
- ping 192.168.64.2
- nmap -sV 192.168.64.2
- nmap -p- -sV 192.168.74.2

## Why an Exposed Service Matters From a Security Perspective
An exposed port is a port that is left open and can be accessed by the public and an exposed port means that the service running on the port is exposed and can be accessed by the public. The more ports that are exposed gives an attacker more ways to get into the system. The service running on the exposed parts may be an outdated version or not set up properly. Running an outdated version of a service means that an attacker could find any vulnerabilities that are known for that version and use it to access the system. Ports that allow users to login or remote access could be vulnerable to brute force attacks.

The VM only has one port open to the public which is port 22 and runs SSH. SSH allows computers to securely access servers and login remotely. The SSH port being left exposed means that an attacker could perform brute force attacks to attempt to access the servers remotely. However because the VM only has one port exposed means that there is only way for an attacker to gain access.

## Compare Nmap and ss
The nmap scan was done from my mac to identify the ports that can be seen from outside the VM and the ss command was run from inside the VM to look for any listening ports. The two commands returned different results when identifying the open ports. The nmap scan that was done from my mac revealed only 1 TCP port and the ss command that was done from inside the VM revealed that there was multiple ports open both UDP and TCP ports.

The nmap scan showed that only port 22 was open and running the SSH service whilst the results of the ss command showed that there was multiple UDP and TCP ports were listening. The ss command showed that the ports that were listening were ports 53 and 22 on both UDP and TCP ports and includes are the DNS and SSH ports. The ss command also showed that the VM was listening on the UDP port 68.

## Ubuntu Firewall
The Ubuntu firewall is called UFW and comes with Ubuntu but is not enabled by default. The purpose of the firewall is to control incoming and outgoing traffic on a computer to prevent unauthorised access. The traffic is controlled by the rules that are set to deny or allow traffic. The firewall can be used allow or deny traffic on specific ports or from specific ip addresses. A firewall can also be used to block or allow traffic from entire networks.

To check the status of the Ubuntu firewall the command sudo ufw status is used. Thos shows the whether the firewall is active or inactive and it shows some of the firewalls rules. To see more information about the firewall like the rules for incoming or outgoing traffic the command sudo ufw status verbose is used. sudo is used to stop everyone from seeing how the firewall is configured and is used to only allow specific people to see how the firewall is configured.

The firewall can be used to restrict access to services by allowing or blocking traffic based on the port numbers or ip addresses. The firewall can block traffic to a port or aloow the traffic to the port. It can also be used to stop traffic from specific ip addresses to a specific port.

## What I have learnt
I have learnt what virtualisation and emulation is. Virtualisation is when the VM runs using the computers physical cpu and emulation is when the software copies and acts as a different cpu to the computer running the software. I used virtualisation because my mac uses apple silicon which is arm based and used the arm based ubuntu server so the VM can run using my macs processor.

I also learnt that the command ip addr returns all the network interfaces and the ip addresses. The output showed 2 interfaces lo and enp0s1. The second interface is the virtual network interface which is used by the VM and is ready to be used. The different details of each interface are also shown like the mtu which is the largest packet size that can be sent over the network, qlen which is how many packets can be queued and the state of the interface.

I have also learnt what the loopback address is. The loopback address is an ip address that is used for a computer to send network packets to itself. This is used for troubleshooting and testing the computers network services

ip route returns the routing table which shows the routing information for the interface. It shows the interface default gateway which is the address that is used to communicate to other networks. ip route show default returns only the interfaces default gateway.

I also learnt that to see all the services on the system the command systemctl is used and to filter for the running services the state flag is used. To see all the ports the command 'ss' is used with different options to filter the output. The options -t and -u filters for the TCP and UDP ports and the option -l filters the ports for only the listening ports. The option -n replaces the port names in the output with their port numbers and the option -p is used to list the names of the processes using the ports.

I have learnt that doing the standard nmap scan by itself it only scans 1000 ports and only tells you the port number and the service running on the port. To see the version of the service running on the ports the option -sV needs to be used. The scan can be used to scan all 65535 ports to check which ports are opened the option -p is used. 

I have also learnt that the amount of ports that can be seen using the nmap scan is different to the ss command. The results of the nmap scan showed less ports listening than the ss command because the nmap scan scans a machine from a different machine to see which ports are open whilst the ss command is used on the same machine that is being scanned and more listening ports can be seen.
