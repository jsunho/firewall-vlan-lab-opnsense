## Overview 

In this part of the project, I install OPNsense inside UTM on my Apple Silicon Mac. OPNsense only supports amd64, so the VM has to run in full x86_64 emulation. It is slower than native ARM virtualization, but for this lab it works completely fine.
The goal here is just to get a basic OPNsense installation running with the three network interfaces I will use later:

  - WAN → UTM Shared Network (NAT)
  - LAN → Internal network (192.168.10.0/24)
  - GUEST → Internal network (192.168.20.0/24)

This installation prepares everything needed for the next steps in the project.

## 1. Requirements

Before I started, I made sure I had:

  - The OPNsense ISO (amd64)
  - UTM installed on macOS (Apple Silicon)
  - Three virtual networks already created in UTM (from 02_utm_setup.md)
    - WAN-Net (Shared)
    - LAN-Net (Isolated)
    - GUEST-Net (Isolated)

## 2. Creating the OPNsense-VM in UTM

Here is how I created the VM:

  1. In UTM, I choose Emulate → Other
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
    
The order matters, because OPNsense usually detects them as em0, em1, and em2.

## 3. Booting into the Installer

After starting the VM, UTM loads the ISO and shows the OPNsense boot menu.
When the live system finishes starting, I get a console login.

Log in with:

  installer / opnsense


## 4. Running the Installer

Inside the installer menu, I chose Install (ZFS).

During the ZFS setup, I selected:

  - stripe (because the VM only has one disk)
  - the only available disk
  - and then confirmed the remaining defaults

OPNsense then installs a ZFS-based system automatically.

## 5. First Boot

When the installation is done:

  - I selected Reboot
  - I removed the ISO from the virtual CD drive in UTM

After reboot, OPNsense loads into the normal console.
Default login:
    
  root / opnsense

## 6. Interface Assignment

From the console menu, I selected:

  1) Assign interfaces

Respond to the prompts:

  Configure LAGGs now?  [y/N]: N
  Configure VLANs now?  [y/N]: N

I answered N to both because I only use plain interfaces.
    
Then OPNsense shows the detected interfaces (usually):

  em0
  em1
  em2

I assigned them like this:

  WAN → em0
  LAN → em1
  GUEST (OPT1) → em2

After confirming, the assignments were applied.

## 7. Automatic IP Addresses

OPNsense automatically configures:
    
    - WAN: DHCP (from UTM Shared Network)
    - LAN: 192.168.1.1/24 (default)

This is enough to access the system for now.

I will change the LAN and GUEST addresses to match the project layout in the next document.


    