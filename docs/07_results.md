## Results and Testing

In this part of the project, I tested whether the network setup and the firewall rules I created earlier actually behave the way I intended.
The goal was to confirm that:

  - the LAN network can access the internet and the firewall
  - the GUEST network gets an IP address and can reach the internet
  - LAN and GUEST cannot talk to each other
  - DNS and ICMP behave correctly
  - the firewall rules match the segmentation

Everything here was tested using two Ubuntu Desktop VMs:
one connected to the LAN network, the other to the GUEST network.

### 1.1 LAN to Firewall WebGUI

From the LAN VM, I opened Firefox and entered:

    https://192.168.10.1

Result: 
  The login page loaded successfully

This confirmes that the LAN network can reach OPNsense.



