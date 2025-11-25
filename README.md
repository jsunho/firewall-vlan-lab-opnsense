# Firewall + VLAN Lab (OPNsense on UTM / macOS M1)

## 1. Overview

This project is a virtual lab environment to practice:
- Deploying an OPNsense firewall as a virtual appliance
- Designing a small multi-VLAN network
- Implementing firewall rules, DHCP, and DNS
- Testing client/server communication across segmented networks

The lab runs on **UTM** on a **macOS M1** host and uses several virtual machines
(OPNsense + Linux clients/servers).

## 2. Goals

- Understand basic firewall and routing concepts
- Implement VLAN-based network segmentation
- Provide separate networks for:
  - Management
  - Clients
  - Servers
- Document the full setup so it can be reproduced by others

## 3. Lab Topology

```text
                Internet
                   |
             [ UTM NAT / Host ]
                   |
                 (WAN)
              [ OPNsense ]
                   |
               (LAN trunk)
                   |
           +-----------------+
           |  UTM internal   |
           |  network        |
           +-----------------+
             |      |      |
          VLAN10  VLAN20  VLAN30
         MGMT    CLIENTS  SERVERS
