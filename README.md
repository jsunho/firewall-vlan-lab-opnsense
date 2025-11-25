# Firewall + VLAN Lab (OPNsense on UTM / macOS M1)

This project documents the creation of a fully virtualized firewall and network segmentation lab using OPNsense, UTM, and multiple isolated virtual networks. It simulates a small-company environment with LAN and GUEST networks, routing, DHCP, and firewall rules.
The goal of this lab is to practice network segmentation, firewall configuration, and multi-network routing in a controlled environment. This project simulates a small business network with restricted guest access and a protected internal LAN.


## 1. Project Overview

The lab consists of three virtual networks connected through an OPNsense firewall:
  - WAN – Internet access through UTM's shared network (NAT)
  - LAN – Primary internal network (192.168.10.0/24)
  - GUEST – Isolated network with restricted access (192.168.20.0/24)

The setup includes:
  - An OPNsense firewall (AMD64, emulated on Apple Silicon)
  - A LAN client (ARM64 Linux VM)
  - A GUEST client (ARM64 Linux VM)

This setup mirrors a real-world small business infrastructure with segmented networks and controlled access.

The lab runs on **UTM** on a **macOS M1** host and uses several virtual machines
(OPNsense + Linux clients/servers).

## 3. Lab Topology

```
          +-----------------------+
          |       macOS Host      |
          +-----------------------+
                   | (NAT)
                   v
            [ WAN - OPNsense ]
                   |
        +----------+-----------+
        |                      |
     [LAN]                 [GUEST]
192.168.10.0/24       192.168.20.0/24
   Client VM              Client VM
```

A full editable diagram is available in:
diagram/network-topology.drawio

## Repository Structure

```
├── README.md
├── docs/
│   ├── 01_intro.md
│   ├── 02_utm_setup.md
│   ├── 03_opnsense_install.md
│   ├── 04_interface_config.md
│   ├── 05_client_vms.md
│   ├── 06_firewall_rules.md
│   ├── 07_results.md
│   └── screenshots/
└── diagram/
    └── network-topology.drawio
```
Each document describes one part of the lab and makes it reproducible.

## Current Status

- [x] UTM environment prepared
- [x] OPNsense installed (ZFS)
- [x] WAN/LAN/GUEST interfaces assigned
- [x] LAN = 192.168.10.1
- [x] GUEST = 192.168.20.1
- [x] WAN via DHCP
- [ ] LAN client VM configured
- [ ] GUEST client VM configured
- [ ] WebGUI access tested
- [ ] DHCP services configured
- [ ] Firewall rules implemented
- [ ] Documentation finalized

## Key Learnings and Concepts

This lab demonstrates:
  - The difference between virtualization (ARM64) and emulation (x86_64)
  - How UTM handles networking (Shared, Bridged, Isolated)
  - Assigning and configuring multiple network interfaces in OPNsense

  - Setting static IPs and IPv4 subnets

  - Routing between networks

  - Creating and testing firewall rules

  - Segmentation between LAN and GUEST VLANs

  - Using a firewall web interface (OPNsense GUI)

  - Understanding DHCP and DNS behavior in segmented networks
  
These skills reflect practical tasks in real IT system integration work.

## Goals of the Project

- Build a functional firewall and multi-network lab
- Understand network segmentation and access control
- Practice using a professional firewall system
- Prepare for real-world IT infrastructure environments
- Document the project clearly and reproducibly

## License

MIT License

## Notes

Some components (especially OPNsense) require x86_64 emulation on Apple Silicon.
This is expected and part of the learning experience.

  

  

  