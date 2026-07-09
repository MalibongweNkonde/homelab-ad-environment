# Phase 1 - Network Design

## Overview

The  goal of this phase was to design a scalable network that would support an enterprise-style Active Directory lab. Rather than placing every device on a single network,the environment was sesegmented into VLANs to separate management, servers, clients, linux and other future services. 

## Objectives

* [x] Build a virtual enterprise network
* [x] Separate traffic using VLANs
* [x] Deploy pfSense as the primary firewall and router
* [x] Provide internet connectivity to the lab
* [x] Prepare the network for Active Directory deployment
* [x] Create room for future services such as monitoring, VPN and a DMZ


## Hardware

| Device | Purpose |
| :--- | :--- |
| Dell Precision M6800| Hosting pfSense and Management virtual machines in KVM/QEMU |
|Desktop Computer| Proxmox Virtualisation platform|
| Huawei Pocket Router | Provides internet to pfSense through M6800 |
| Cuddy wr1200 | Was planned to be used as a switch between the laptop and desktop |


## Virtual Machines

|VM | Role |
|:---|:---|
| pfSense | Router, Firewall, DHCP |
| Manangement VM | Administration workstation for devices on LAN|
| Proxmox Host | Hypervisor for Active Directory and related services |

## Network Topolgy

| VLAN | Name | Subnet | Purpose |
| :--- | :--- | :--- | :--- |
| 1 | Management | 10.0.0.0/24 | Proxmox and infrastructure management |
| 20 | Servers | 10.0.20.0/24 | Active Directory and server workloads |
| 30 | Workstations | 10.0.30.0/24 | Windows client machines |
| 40 | Linux | 10.0.40.0/24 | Linux services |
| 50 | DMZ | 10.0.0.50/24 | Public facing services |
| 60 | Guest | 10.0.60.0/24 |  Isolated guest network |

## IP Addressing
| Device| IP Address|
| :---| :--- |
| pfSense VM |10.0.0.1|
| Proxmox Host | 10.0.0.10|
| Management VM | 10.0.0.20|
| Domain Coontroller | To be set up**|

## Internet Connectivity

Internet connection is provided by the Huawei Pocket router connected wirelessly to the Dell Precision M6800.

Wifi &rarr; Linux Host Operating System &rarr; pfSense WAN &rarr; pfSense LAN &rarr; Proxmox Virtual Networks &rarr; Virtual Machines

## Security Considerations

- Separate management traffic from user traffic.
- rerserve static IP addresses for infrastructure servers.
- Restrict administrative access to the management VLAN.
- Prepare for future firewall rules between VLANs.
- Minimize unnnceassary communication between segments



## Challenges Encountered

| Problem | Investigation | Resolution | LessonLearned |
| :--- | :--- | :--- | :--- |
|Bridge on M6800 host OS| Bridge would dissapear on every restart| Removed the duplicate entries of bridge from nmtui. <br> Removed existing bridges stored in 'cd /etc/NetworkManager/system-connections/'.<br> Created new permanent bridge using nmcli.| nmtui does not create a permanent brdige. <br> Clear old bridge configuration to avoid potential conflict.|
|DNS| Management PC could not connect to internet but could ping 8.8.8.8 and pfSense|I ran commands:<br> 'sudo nmcli connection show'<br> 'sudo nmcli connection modify "connection name" ipv4.dns "pfsense ip"'<br> 'sudo nmcli connection up "connection name"' <br> to set the DNS server to pfSense| It is always DNS|
|||||
|||||

## Skills Demonstrated 

- Network Design
- IP Addressing
- VLAN Planning
- pfSense Configuration
- Proxmox Networking
- Linux Networking
- Troubleshooting
- Documentation
