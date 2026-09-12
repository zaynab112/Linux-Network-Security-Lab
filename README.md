# Linux-Network-Security-Lab
A practical lab demonstrating Linux administration, Networking, Service discovery and Security hardening.

The objective of this project is to build a Linux environment and demonstrate Linux administration, networking, discovering services and improve security.

## Creating Linux VM

I chose to use Ubuntu server as the operating system because it is a lightweight terminal that will allow me to develop my linux and networking fundamentals.

### Configurations
Virtualisation - I chose virtualisation because I downloaded the arm 64 version as my mac processor is arm based. This allows Ubuntu to run using my macs processor rather than having to copy and act as a different processor.

Ram - I gave the ubuntu server 2GB RAM because it is lightweight so doesn't require as much memory. This was enougn memory to practice linux commands and networking tasks.

Storage - I gave the VM 30GB storage to have enough for the software, files and the server.

## Issues
When installing Ubuntu I had two issues:
- The installation of Ubuntu kept failing as I did not create a virtual hard drive for it to install to. This meant that the system could detect a disk to install Ubuntu so it kept failing. To resolve this I created the virtual drive.
- Once installed the system kept going to the 'try or install Ubuntu' page. This was because the installer file was still in the system so it kept loading up that file. To resolve this I removed the installer file and kept the virtual disk meaning when the system was starting it started the system correctly. 

## Commands Used
- sudo apt update - checks for updates
- hostname - returns the name of the machine
- ip addr - returns all the network interfaces and their ip addresses
- ip route - returns the routing table
- ip route show default - only returns the VMs default gateway
- systemctl list-units --type=service --state=running - returns a list of all the running services
- ss -tuln - returns all the ports that are listening using TCP or UDP

## VM details
- Hostname: linuxlab
- ip address: 192.168.64.2
- Network Interface: enp0s1
- Default Gateway: 192.168.64.1

## Services and Ports
<img width="802" height="334" alt="Screenshot 2026-09-10 at 16 04 05" src="https://github.com/user-attachments/assets/75fd90e1-9850-46e2-9f23-4c40a37c8c8f" />

This shows the output of the command systemctl using the state flag which filters the results for only the services that are currently running on the system. Without the state flag the output would include all the services on the system even if they're not running. The output shows the name of the service, the state of the service and a description of what the service does.

<img width="1194" height="205" alt="Screenshot 2026-09-10 at 16 17 13" src="https://github.com/user-attachments/assets/3222ff26-be1d-4cef-8061-56360e4331ed" />
This shows the output of the command ss with the options -t, -u, -l, -n. The options filter for the listening ports that are either TCP or UDP ports. The output shows the type of ports, the state of the ports and the port numbers. The output also shows how many packets have been recievd and how many packets are in queue to be sent. In this case no packets have been received by either the TCP or UDP ports and only the TCP ports have packets in queue to be sent. It also shows that DNS uses both TCP and UDP ports.

## What I have learnt
I have learnt what virtualisation and emulation is. Virtualisation is when the VM runs using the computers physical cpu and emulation is when the software copies and acts as a different cpu to the computer running the software. I used virtualisation because my mac uses apple silicon which is arm based and used the arm based ubuntu server so the VM can run using my macs processor.

I also learnt that the command ip addr returns all the network interfaces and the ip addresses. The output showed 2 interfaces lo and enp0s1. The second interface is the virtual network interface which is used by the VM and is ready to be used. The different details of each interface are also shown like the mtu which is the largest packet size that can be sent over the network, qlen which is how many packets can be queued and the state of the interface.

ip route returns the routing table which shows the routing information for the interface. It shows the interface default gateway which is the address that is used to communicate to other networks. ip route show default returns only the interfaces default gateway.

I also learnt that to see all the services on the system the command systemctl is used and to filter for the running services the state flag is used. To see all the ports the command 'ss' is used with different options to filter the output. The options -t and -u filters for the TCP and UDP ports and the option -l filters the ports for only the listening ports. The option -n replaces the port names in the output with their port numbers and the option -p is used to list the names of the processes using the ports.
