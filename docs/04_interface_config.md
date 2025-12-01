## Interface Configuration

After the initial installation, the default OPNsense interface configuration must be adapted to match the project’s network design. This includes setting static IPv4 addresses for the LAN and GUEST networks, enabling DHCP services where required, and preparing the system for client connectivity.

## 1. Overview of Required Network Layout

The following addresses will be applied:

  - LAN: 192.168.10.1/24
  - GUEST: 192.168.20.1/24
  - WAN: DHCP (no change)

These values correspond to the network plan defined in the project structure.

## 2. Accessing the Console Menu

At the OPNsense console, select:

  2) Set interface IP address

The system will ask which interface should be configured.

## 3. Configuring the LAN Interface (em1)

Select LAN when prompted.

Apply the following values:

  - IPv4 address: 192.168.10.1
  - Subnet mask: /24
  - IPv6 configuration: none
  - Enable DHCP server on LAN: N
  - Revert to HTTP instead of HTTPS: N

The console will apply the configuration and display the new LAN address.

## 4. Configuring the GUEST Interface (OPT1 / em2)

Run the same menu option again:

  2) Set interface IP address

Select OPT1.

Apply the following values:

  - IPv4 address: 192.168.20.1
  - Subnet mask: /24
  - IPv6 configuration: none
  - Enable DHCP server on OPT1: N
  - Revert to HTTP instead of HTTPS: N

After confirmation, the new interface configuration becomes active.

## 5. Verifying the Configuration

To view the current interface assignments, select:

  1) Assign interfaces

Expected result:

  - LAN (em1) → 192.168.10.1/24
  - OPT1 (em2) → 192.168.20.1/24
  - WAN (em0) → DHCP

If the addresses match, the system is ready for WebGUI access.

## 6. Accessing the WebGUI

The OPNsense WebGUI is not accessed from the firewall console.
To continue, switch to the LAN client VM, which will be prepared in the next chapter.
Once the client is configured and connected to the LAN-Net, the WebGUI can be opened at:

  - https://192.168.10.1

