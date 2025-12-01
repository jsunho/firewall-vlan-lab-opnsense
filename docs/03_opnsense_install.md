## Overview 

This document explains how to install OPNsense inside UTM on an Apple Silicon Mac.
Because OPNsense only supports amd64, the VM runs in full x86_64 emulation, which is slower than native ARM virtualization but fully adequate for a lab environment. The goal is to prepare a minimal but functional firewall with the three required interfaces:

    - WAN → UTM Shared Network (NAT)
    - LAN → Internal network (192.168.10.0/24)
    - GUEST → Internal network (192.168.20.0/24)

This installation is the foundation for later configuration steps in the lab architecture shown in the repository overview.

## 1. Requirements

Before starting, the following components are required:

    - The OPNsense ISO (amd64)
    - UTM installed on macOS (Apple Silicon)
    - Three virtual networks already created in UTM (from 02_utm_setup.md)
        - WAN-Net (Shared)
        - LAN-Net (Isolated)
        - GUEST-Net (Isolated)

## 2. Creating the OPNsense-VM in UTM

Create a new VM in UTM:

    1. Choose Emulate → Other
    2. CPU settings:
        - Architecture: x86_64
        - Cores: 4
        - Memory: 4096 MB
    3. Other:
        - Attach the OPNsense ISO.
    4. Storage:
        - Create a 16-32 GB virtual disk.
    5. Networking (three NICs, assigned in order):
        - NIC 1 → WAN-Net (Shared to macOS)
        - NIC 2 → LAN-Net
        - NIC 3 → GUEST-Net
    
The order matters: OPNsense typically detects the adapters as em0, em1, em2.

## 3. Booting into the Installer

Start the VM. UTM loads the ISO and the OPNsense boot menu appears.
After the live system finishes booting, the console login prompt becomes available.

Log in with:

    User: installer
    Password: opnsense

## 4. Running the Installer

Select Install (ZFS) from the installer menu.
During the ZFS configuration workflow:

    - Select stripe as the virtual device type (sinlge disk)
    - Select the only available disk
    - Confirm all remaining defaults

The installer creates a standard ZFS layout suitable for OPNsense in a virtual machine.

## 5. First Boot

After installation finishes: 

    - Select Reboot
    - Remove the ISO from the virtual CD drive in UTM

OPNsense boots into the console with the standard menu.

Default login:
    
    - User: root
    - Password: opnsense

## 6. Interface Assignment

Select:

    - 1) Assign interfaces

Respond to the prompts:

    - Configure LAGGs now?  [y/N]: N
    - Configure VLANs now?  [y/N]: N
    
The system then displays the detected interfaces, typically:

    - em0
    - em1
    - em2

Assign the interfaces as follows:

    - WAN → em0
    - LAN → em1
    - GUEST (OPT1) → em2

Confirm and apply the configuration.

## 7. Automatic IP Addresses

OPNsense automatically configures:
    
    - WAN: DHCP (from UTM Shared Network)
    - LAN: 192.168.1.1/24 (default)

These defaults are sufficent for initial access. 
Final network settings will be adjusted in the next doucment.


    