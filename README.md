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
- ip addr - returns all the VMs interfaces and their ip addresses
- ip route - returns the routing table
- ip route show default - only returns the VMs default gateway

## VM details
- Hostname: linuxlab
- ip address: 
- Network Interface: 
- Default Gateway: 192.168.64.1

## Services and Ports

## What I have learnt
