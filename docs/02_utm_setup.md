## UTM Environment Preparation

This lab uses UTM on macOS to create an isolated virtual network environment consisting of one firewall VM and two client VMs. UTM provides all necessary virtual switches, NAT services, and interface mappings without affecting the host system.
Because OPNsense requires an x86_64 environment, the firewall VM is executed using full emulation.
The client VMs run natively as ARM64 Linux machines.

## Virtual Networks

Three separate virtual networks are created inside UTM to simulate a multi-segment infrastructure:

### 1. WAN Network
Mode: Shared Network (NAT)
Purpose: Provide external connectivity via macOS
Assigns IP to OPNsense automatically through DHCP
Used only by the firewall VM

![WAN interface assignment](screenshots/utm_settings_network_wan.png)

### 2. LAN Network
Mode: Isolated Network
Used by the trusted LAN client VM
Connected to OPNsense as its primary internal interface

![LAN interface assignment](screenshots/utm_settings_network_lan.png) 

### 3. GUEST Network
Mode: Isolated Network
Used by the guest client VM
Connected to OPNsense as a restricted interface

![GUEST interface assignment](screenshots/utm_settings_network_guest.png)

The LAN and GUEST networks are isolated from each other at the UTM level; all routing between them is controlled by OPNsense.


## OPNsense VM Setup in UTM

### Hardware Configuration
    - Architecture: x86_64 (emulated)
    - Memory: 2–4 GB (depending on host resources)
    - CPU: 2 cores recommended
    - Disk: 16–32 GB
    - Boot ISO: OPNsense installation image

![OPNsense VM architecture](screenshots/utm_firewall_vm_architecture.png)

### Network Interfaces (in order)
    - em0 → WAN (Shared Network)
    - em1 → LAN (Isolated Network)
    - em2 → GUEST (Isolated Network)

This order ensures the interfaces match the addressing plan later on.

## Client VMs

Two lightweight Linux VMs are prepared:

### LAN Client
    - Architecture: x84_64
    - Network: LAN isolated network
    - Receives IP via DHCP from OPNsense
### GUEST Client
    - Architecture: x84_64
    - Network: GUEST isolated network
    - Receives IP via DHCP from OPNsense

These machines are used to verify segmentation, firewall behavior, and DNS/Internet functionality.

## Summary

At this stage, the UTM environment provides the following:
    - Three isolated virtual networks
    - One emulated OPNsense firewall VM connected to all networks
    - Two client VMs connected to their respective LAN and GUEST networks
    - A clean foundation for further installation and configuration steps
    
This setup mirrors the topology of a small-business network with separate trusted and guest environments.