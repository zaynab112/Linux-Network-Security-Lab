# Linux-Network-Security-Lab
A practical lab demonstrating Linux administration, Networking, Service discovery and Security hardening.

The objective of this project to build a Linux environment and demonstrate Linux administration, networking, discovering services and improve security.

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
- hostname - returns the name of the machine
- ip addr - returns all the network interfaces and their ip addresses
- ip route - returns the routing table
- ip route show default - only returns the VMs default gateway
- systemctl list-units --type=service --state=running - returns a list of all the running services
- ss -tuln - returns all the ports that are listening using tcp or udp

## VM details
- Hostname: linuxlab
- ip address: 192.168.64.2
- Network Interface: enp0s1
- Default Gateway: 192.168.64.1

## Services and Ports


## What I have learnt
I have learnt what virtualisation and emulation is. Virtualisation is used when the architecture of the VM is the same as the computers processor and emulation is used when the computers processor is different to the VMs architecture so the system needs to copy the behaviour of the VMs system. I used virtualisation because my mac uses apple silicone which is arm based and used the arm based ubuntu server so the VM can run using my macs processor.

I also learnt that the command ip addr returns all the network interfaces and the ip addresses. The output showed 2 interfaces lo and enp0s1. The second interface is the virtual network interface which is used by the VM and is ready to be used. The different details of each interface are also shown like the mtu which is the largest packet size that can be sent over the network, qlen which is how many packets can be queued and the state of the interface.

ip route returns the routing table which shows the routing information for the interface. It shows the interface default gateway which is the address that is used to communicate to other networks. ip route show default returns only the interfaces default gateway.
