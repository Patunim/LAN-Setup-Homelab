# LAN-Setup-Homelab
Objective
This lab was designed to simulate a small office LAN environment. The goal? Connect three wired PCs, a printer, and a wireless laptop all under a functioning local area network. DHCP services would be handled by a single router, allowing seamless IP assignment and enabling device-to-device communication. A wireless router was integrated to connect mobile devices like laptops to the network.

Tools Used: Cisco Packet Tracer
Focus Areas: DHCP Configuration, IP Addressing, Wired & Wireless Integration, Device Connectivity Testing.

Lab Topology

End Devices:

PC-0

PC-1

PC-2

Laptop-0

Printer-0

Networking Devices:

Router-0

Switch-0

WirelessRouter-0

Step-by-Step Instructions

1. Add Devices to the Workspace

Open Cisco Packet Tracer and drag the following components into the workspace:

From End Devices:
- PC-0
- PC-1
- PC-2
- Laptop-0
- Printer-0

From Network Devices:
- Router-0
- Switch-0
- WirelessRouter-0

2. Physical Connections

Wired Connections

Use copper straight-through cables to connect:

PC-0 → Switch Port FastEthernet 0/1

PC-1 → FastEthernet 0/2

PC-2 → FastEthernet 0/3

Printer → FastEthernet 0/4

Router GigabitEthernet 0/0 → Switch FastEthernet 0/5

Wireless Router Connection

Use a crossover cable to connect:

WirelessRouter-0 Internet Port → Router GigabitEthernet 0/1

3. Router Configuration

Open CLI on Router-0 and input the following:
```
enable
configure terminal
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface gigabitEthernet 0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
ip dhcp pool LAN
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
exit
ip dhcp pool WLAN
network 192.168.2.0 255.255.255.0
default-router 192.168.2.1
exit
do wr
```
4. Wireless Router Configuration (GUI Mode)

Go to GUI > Setup

Set Internet Connection Type to DHCP

Under Wireless Settings:

SSID: SmallOfficeWiFi

Security: WPA2-PSK

Passphrase: office123

Under LAN Settings:

IP: 192.168.2.1

Subnet Mask: 255.255.255.0

Enable DHCP Server (on 192.168.2.0/24)

5. End Device Configuration

For Wired PCs (PC-0, PC-1, PC-2)

Desktop > IP Configuration

Set to DHCP mode.

For Printer

Assign a static IP outside the DHCP pool range.Example:
```
IP Address: 192.168.1.101
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server: 192.168.1.1 or 8.8.8.8
```
For Wireless Laptop

Desktop > IP Configuration > DHCP

Config Tab > Wireless0

Select SmallOfficeWiFi, enter password office123, and connect.

Testing & Verification

From PC-0:

ipconfig
ping 192.168.1.1

Should get IP from DHCP (192.168.1.x)

Should be able to ping the router (192.168.1.1)

From Laptop-0:
```
ipconfig
ping 192.168.2.1
```
Should receive IP in the 192.168.2.x range

Confirm wireless router is reachable

From Any PC:
```
ping 192.168.1.101
```
Test if the printer responds to ping.

Confirms all wired devices can communicate.

Key Takeaways

Practical setup of both wired and wireless LANs in a single network

Implemented and tested DHCP pools for two different subnets

Understood static vs dynamic IP addressing in enterprise networks

Reinforced hands-on CLI command skills and router/switch configuration

Verified full end-to-end connectivity for devices across subnets
