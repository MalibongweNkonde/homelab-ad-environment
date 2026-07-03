# homelab-active-directory-environment

## Overview
This repository documents a self-hosted enterprise homelab built to simulate a small business network.

## Technologies
- Proxmox VE
- KVM/QEMU
- pfSense
- DNS
- DHCP
- Pi-hole
- WireGuard
- Windows Server 2019
- Debian, Ubuntu Linux
- Active Directory

## Objectives
- Deploy Active Directory
- Deploy a ticketing system
- Configure DNS and DHCP
- Build a segmented VLAN network
- Secure the network using pfSense
- Practice Group Policy management
- Deploy Linux Servers
- Configure remote VPN access
- Simulate real world enterprise administration

## Hardware
### Host 1 [Dell Precision M6800]
* **CPU:** Intel i7-4600M
* **RAM:** 16GB
* **DISK:** 160GB Boot drive; 500GB secondary drive
* **NICs:** Built in Gigabit Ethernet port

### Host 2 [Desktop Computer]
* **CPU:** Intel i7-4790
* **RAM:** 16GB
* **DISK:** 500GB SSD
* **NICs:** Built in Gigabit Ethernet port

## Network topology:
* **WAN:** DHCP (ISP Modem)
* **LAN:** 10.0.0.0/24 (Management)
* **VLAN 20 (Servers):** 10.0.20.0/24
* **VLAN 30 (Workstations):** 10.0.30.0/24 (DHCP)
* **VLAN 40 (Linux):** 10.0.40.0/24
* **VLAN 50 (DMZ):** 10.0.50.0/24
* **VLAN 60 (Guest):** 10.0.60.0/24

## Interface Assignments
### Management
    **pfSense:** 10.0.0.1
    **Proxmox:** 10.0.0.10
    **Management PC:** 10.0.0.20
### Servers
    **Domain Controller:** 10.0.20.10
    **Secondary DC:** 10.0.20.11
    **File Server:** 10.0.20.20
    **SQL Server:**10.0.20.30
### Workstations
    **Windows Client 1:** DHCP
    **WIndows Client 2:** DHCP
    **Windows Client 3:** DHCP
### Linux
    **Ubuntu Server** 10.0.40.10
    **Monitoring Server** 10.0.40.20
    **Docker Host** 10.0.40.30

### DMZ
    **Unused for now**
    
### Guest
    **Smartphone:** DHCP
    **Laptop:** DHCP

## Installed Packages
- **pfBlockerNG-devel:** DNSBL and IP filtering.
- **Snort/Suricata:** Intrusion Detection/Prevention (IDS/IPS).
- **WireGuard:** Remote access VPN.
- **Avahi:** mDNS reflector for IoT devices.

## Configuration Notes
- **DNS Resolver:** Configured with DNS over TLS via Cloudflare (1.1.1.1).
- **Firewall Rules:** Blocked IoT VLAN from accessing LAN and pfSense WebGUI.
- **DHCP:** Pools configured for all VLANs with static mappings for servers.

