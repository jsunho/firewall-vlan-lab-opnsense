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

## 3. Configuring the LAN Interface (em1)

When I select the LAN interface, OPNsense asks a few questions.
I entered the following values:

  - IPv4 address: 192.168.10.1
  - Subnet mask: /24
  - IPv6 configuration: none
  - Enable DHCP server on LAN: Y
  - Range: 192.168.10.50 - 192.168.10.200
  - Revert to HTTP instead of HTTPS: N

Once confirmed, OPNsense updates the LAN address.

## 4. Configuring the GUEST Interface (OPT1 / em2)

To configure the GUEST interface, I repeated the same menu option:

  2) Set interface IP address

Then I select OPT1.

Here I entered:

  - IPv4 address: 192.168.20.1
  - Subnet mask: /24
  - IPv6 configuration: none
  - Enable DHCP server on OPT1: N
  - Revert to HTTP instead of HTTPS: N

After confirming, the new IP for the GUEST network becomes active.

## 5. Verifying the Configuration

To make sure everything is set correctly, I opened the menu:

  1) Assign interfaces

Here OPNsense shows the current interface assignments.
It should look like this:

  - LAN (em1) → 192.168.10.1/24
  - OPT1 (em2) → 192.168.20.1/24
  - WAN (em0) → DHCP

If these values match, the interface setup is complete.

## 6. Accessing the WebGUI

The WebGUI cannot be opened from the firewall console itself.
To continue, I switch to the LAN client VM (configured in the next chapter).
Once that VM is connected to LAN-Net, I can open the OPNsense WebGUI in a browser:

  https://192.168.10.1

This is the address I will use to continue the setup in the next part of the project.
