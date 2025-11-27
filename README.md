# Firewall + VLAN Lab (OPNsense on UTM / macOS M1)

This project documents a fully isolated network lab using OPNsense, UTM, and multiple virtual networks.
The environment simulates a small-business infrastructure with segmented LAN and GUEST networks, firewall rules, DHCP, DNS, and controlled routing paths.

The goal of this lab is to practice real-world system integration skills: network design, segmentation, firewall administration, virtualization, and troubleshooting.


## 1. Architecture Overview

The lab consists of:
  - 1× OPNsense Firewall (amd64, emulated on Apple Silicon)
  - 1× LAN client VM (ARM64 Linux)
  - 1× GUEST client VM (ARM64 Linux)
  - 3 virtual networks in UTM:
    - WAN → NAT to macOS (internet access)
    - LAN → internal network (trusted)
    - GUEST → isolated network (restricted)

This setup mirrors infrastructure commonly found in small and medium-sized organizations.

## 2. Network Topology

```
               +-------------------------+
               |        macOS Host       |
               |   (UTM Shared Network)  |
               +-----------+-------------+
                           |
                        [ WAN ]
                           |
                     +-----+-----+
                     | OPNsense  |
                     +-----+-----+
                           |
               +-----------+-----------+
               |                       |
            [ LAN ]                 [ GUEST ]
        192.168.10.0/24           192.168.20.0/24
            Linux VM                  Linux VM

```

A full editable diagram is available in:
diagram/network-topology.drawio

## 3. Addressing Plan

LAN Network
  - Subnet: 192.168.10.0/24
  - Gateway: 192.168.10.1 (OPNsense LAN interface)
  - DHCP: provided later by OPNsense
  - Purpose: main internal network for trusted clients

GUEST Network
  - Subnet: 192.168.20.0/24
  - Gateway: 192.168.20.1 (OPNsense OPT1 interface)
  - DHCP: provided later by OPNsense
  - Purpose: isolated guest environment with restricted access

WAN Network
  - Provided by UTM (NAT)
  - DHCP from host → used for internet access

## 4. Repository Structure

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

## 5. Current Status

- [x] UTM environment prepared
- [x] OPNsense installed (ZFS)
- [x] WAN/LAN/GUEST interfaces assigned
- [x] LAN = 192.168.10.1
- [x] GUEST = 192.168.20.1
- [x] WAN via DHCP
- [x] LAN client VM configured
- [x] GUEST client VM configured
- [x] WebGUI access tested
- [x] DHCP services configured
- [x] Firewall rules implemented
- [ ] Documentation finalized

## 6. Key Learnings and Concepts

During the project I worked with:
  - Virtualization vs. emulation on Apple Silicon
  - UTM networking (Shared vs. Isolated mode)
  - Assigning interfaces in OPNsense (em0, em1, em2)
  - Static IP configuration and subnetting
  - DHCP, DNS, and routing fundamentals
  - Writing firewall rules (allow/deny policies, segmentation)
  - Testing connectivity (ping, traceroute, DNS tests)
  - Using and securing the OPNsense WebGUI
  - Creating reproducible documentation

These are all relevant to real-world system administration and system integration work.

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

  

  

  