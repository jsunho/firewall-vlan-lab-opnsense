## Interface Configuration

After installing OPNsense, I needed to change the default interface settings so they match the network layout of this project. In this step, I set the IP addresses for the LAN and GUEST networks. These addresses will later be used by the client VMs and by the firewall rules.

## 1. Overview of Required Network Layout

For this lab, I use the following IP addresses:

  - LAN: 192.168.10.1/24
  - GUEST: 192.168.20.1/24
  - WAN: DHCP (no change)

This is the addressing plan I use throughout the project.

## 2. Accessing the Console Menu

Inside the OPNsense console menu, I selected:

  2) Set interface IP address

After that, OPNsense asks which interface I want to configure.

## 3. Configuring the LAN Interface (vtnet1)

When I select the LAN interface, OPNsense asks a few questions.
I entered the following values:

  - IPv4 address: 192.168.10.1
  - Subnet mask: /24
  - IPv6 configuration: none
  - Enable DHCP server on LAN: Y
  - Range: 192.168.10.50 - 192.168.10.200
  - Revert to HTTP instead of HTTPS: N

Once confirmed, OPNsense updates the LAN address.

## 4. Configuring the GUEST Interface (OPT1 / vtnet2)

To configure the GUEST interface, I repeated the same menu option:

  2) Set interface IP address

Then I select OPT1.

Here I entered:

  - IPv4 address: 192.168.20.1
  - Subnet mask: /24
  - IPv6 configuration: none
  - Enable DHCP server on OPT1: Y
  - Range: 192.168.20.50 - 192.168.20.200
  - Revert to HTTP instead of HTTPS: N

After confirming, the new IP for the GUEST network becomes active.

## 5. DHCP Server Configuration

After setting the IP addresses for the LAN and OPT1 interfaces, I needed to make sure that only one DHCP service is active. OPNsense provides two different DHCP systems: ISC DHCPv4 and Dnsmasq.
For this project, I use ISC DHCPv4 only, because it is automatically enabled when I select “Enable DHCP” during the console setup.

To avoid conflicts, I keep Dnsmasq DHCP disabled. If both DHCP services try to run on the same interface, ISC DHCPv4 cannot start and shows the error “address already in use”. In that case, the clients would fail to receive an IP address and would fall back to a 169.254.x.x address.

By keeping Dnsmasq DHCP turned off, I ensure that ISC DHCPv4 runs correctly on both LAN and OPT1, and that the client VMs can obtain their IP addresses without any issues.

## 6. Verifying the Configuration

To make sure everything is set correctly, I opened the menu:

  1) Assign interfaces

Here OPNsense shows the current interface assignments.
It should look like this:

  - LAN (vtnet1) → 192.168.10.1/24
  - OPT1 (vtnet2) → 192.168.20.1/24
  - WAN (vtnet0) → DHCP

If these values match, the interface setup is complete.

## 7. Accessing the WebGUI

The WebGUI cannot be opened from the firewall console itself.
To continue, I switch to the LAN client VM (configured in the next chapter).
Once that VM is connected to LAN-Net, I can open the OPNsense WebGUI in a browser:

  https://192.168.10.1

This is the address I will use to continue the setup in the next part of the project.
