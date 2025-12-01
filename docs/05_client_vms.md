## Client VM Setup

To test the firewall and to work with the OPNsense WebGUI, I created two Ubuntu Desktop VMs.
Each one is connected to a different internal network so I can check later whether my firewall rules work as expected.

  - One connected to the LAN network
  - One connected to the GUEST network

Ubuntu Desktop works well for this because it already includes a graphical interface and Firefox.

## 1. Creating the Client VMs in UTM

I created two separate VMs in UTM:

### LAN Client VM

  - Connected to LAN-Net
  - Ubuntu Desktop (ARM64) installation

### GUEST Client VM

  - Connected to GUEST-Net
  - Ubuntu Desktop (ARM64) installation

For both VMs, I used the same basic settings:

  - 2 CPU cores
  - 2048 - 4096 MB RAM
  - 16 -32 GB disk
  - Network interface attached to the corresponding isolated UTM network

I did not need any special configuration during installation.

## 2. Network Connectivity

After Ubuntu finished installing, I booted each VM to check if it was really connected to the correct network.

### LAN Client

Inside the LAN VM, I opened a terminal and ran:

    ip a

I expected to see:
  
  - Interface (usually enp0s1)
  - IP address in the range 192.168.10.x

![LAN VM IP](screenshots/lan_vm_ip_a.png)

### GUEST Client

For the GUEST VM, the process is exactly the same.
Later, after DHCP is configured, this VM should get an IP in the 192.168.20.x range.

## 3. Accessing the OPNsense WebGUI from the LAN Client

Once the LAN client had a correct IP address, I opened Firefox and went to:

  https://192.168.10.1

OPNsense uses a self-signed certificate, so Firefox warns about it.
I continued to the site.

![Accessing WebGUI](screenshots/lan_vm_access_webgui.png)

Login with:

  root / opnsense

After logging in, the OPNsense dashboard appeared.

## 4. Preparing for DHCP Configuration

Before setting up any firewall rules, I first needed to make sure that the clients can reach the firewall and open the WebGUI.
At this stage, the client VMs only need:
  
  - A connection to the correct network
  - A browser to access the firewall
  - The ability to reach the WebGUI

Full DHCP and DNS configuration will be done in the next chapter.

![WebGUI Dashboard](screenshots/lan_vm_opnsense_dashboard.png)

