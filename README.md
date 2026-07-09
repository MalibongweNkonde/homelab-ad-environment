# homelab-active-directory-environment

## Overview

This repository documents a self-hosted enterprise homelab built to simulate a small business network.

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

# Network Architecture

This diagram shows the phhysical and virtual design of the homelab environment, including the pfSense firewall, Proxmox host, VLAN segmentation, and virtual machines

![Network Architecture](doc/images/network-architecture.png)


## Hardware

| Host 1 |[Dell Precision M6800]|
| :---| :---|
| **CPU:** | Intel i7-4600M|
| **RAM:** | 16GB|
| **DISK:** | 160GB Boot drive; 500GB secondary drive |
| **NICs:** | Built in Gigabit Ethernet port |

| Host 2 |[Desktop Computer] |
| :--- | :--- |
| **CPU:** |Intel i7-4790 |
| **RAM:** |16GB |
| **DISK:** | 500GB SSD |
| **NICs:** | Built in Gigabit Ethernet port |

| Network topology |  |
| :--- | :--- |
|* **WAN:** |DHCP (ISP Modem) |
|* **LAN:** |10.0.0.0/24 (Management) |
|* **VLAN 20 (Servers):**| 10.0.20.0/24 |
|* **VLAN 30 (Workstations):**| 10.0.30.0/24 (DHCP) |
|* **VLAN 40 (Linux):** | 10.0.40.0/24 |
|* **VLAN 50 (DMZ):** | 10.0.50.0/24 |
|* **VLAN 60 (Guest):** | 10.0.60.0/24 |

## Interface Assignments
### Management
    pfSense: 10.0.0.1
    Proxmox: 10.0.0.10
    Management PC: 10.0.0.20
### Servers
    Domain Controller: 10.0.20.10
    Secondary DC: 10.0.20.11
    File Server: 10.0.20.20
    SQL Server: 10.0.20.30
### Workstations
    Windows Client 1: DHCP
    WIndows Client 2: DHCP
    Windows Client 3: DHCP
### Linux
    Ubuntu Server: 10.0.40.10
    Monitoring Server: 10.0.40.20
    Docker Host: 10.0.40.30

### DMZ
    Unused for now
    
### Guest
    Smartphone: DHCP
    Laptop: DHCP

## Github File Structure

    ├── diagrams
    ├── docs
    │   ├── 01-network-design.md
    │   ├── 02-pfsense-setup.md
    │   ├── 03-proxmox-installation.md
    │   ├── 04-active-directory.md
    │   ├── 05-pihole.md
    │   ├── 06-wireguard-vpn.md
    │   ├── 07-ticket-system.md
    │   └── troubleshoot.md
    ├── README.md
    ├── screenshots
    └── scripts
        ├── bash
        ├── powershell
        └── python


## Technologies used
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

## Installed Packages
- **N/A:** 

## Configuration Notes
- **Firewall Rules:** Blocked """""" VLAN from accessing LAN and pfSense WebGUI.
- **DHCP:** Pools configured for all VLANs with static mappings for servers.

## Project Progress

- [x] Install pfSense
- [x] Configure VLANs
- [x] Install Proxmox
- [] Install Windows Server
- [] Promote Domain Controller
- [] Create Active Directory users
- [] Configure Group Policy
- [] Deploy Wireguard
- [] Install Pi-hole

