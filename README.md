# 🌐Enterprise Campus Network Architecture

A hands-on networking project built using **Cisco Packet Tracer**, demonstrating how to design, configure, troubleshoot, and validate a segmented campus network connected to an ISP-style network.

The project focuses on practical networking concepts, including VLAN segmentation, inter-VLAN routing, Multi-Area OSPF, HSRP, DHCP relay, and simulated web services.

It also demonstrates a structured troubleshooting approach, following network traffic from end-user devices to remote servers and identifying configuration issues across different network layers.

---

## 📌 Project Overview

| Category | Details |
|---|---|
| Simulation Tool | Cisco Packet Tracer 9.0.1 |
| Network Type | Campus-to-ISP Network |
| VLANs | 10, 20, 30, 40 |
| Routing Protocol | OSPF (Multi-Area) |
| Redundancy | HSRP |
| IP Address Assignment | DHCP |
| Network Services | DHCP and HTTP |
| WAN Connectivity | Two /30 point-to-point links |

## 🏗️ Network Topology

![Campus Network Topology]

The topology consists of a segmented campus network connected to an ISP-style network through two WAN links.

The campus network uses two multilayer switches to provide VLAN segmentation and inter-VLAN routing, while two edge routers connect the campus to the external simulated network.

The green network contains five interconnected routers and three simulated web servers.

## ⚙️ Technologies & Networking Concepts

- **VLANs:** Segmentation of the campus network into four departments.
- **Inter-VLAN Routing:** Communication between different VLANs using multilayer switches.
- **HSRP:** Virtual gateway configuration for network redundancy.
- **OSPF:** Dynamic routing using Area 0 and Area 2.
- **DHCP:** Dynamic IP address assignment for end-user devices.
- **DHCP Relay:** Forwarding DHCP requests between client VLANs and the DHCP server.
- **WAN Connectivity:** Two separate point-to-point WAN connections.
- **HTTP:** Testing access to simulated web servers.
- **Troubleshooting:** Identifying Layer 2, Layer 3, routing, and DHCP configuration issues.

## 🗂️ IP Addressing & VLAN Configuration

All user VLANs use a `/26` subnet mask (`255.255.255.192`).

| VLAN | Department | Network | HSRP Gateway |
|---|---|---|---|
| 10 | HR | 10.0.0.0/26 | 10.0.0.3 |
| 20 | PR | 10.0.0.64/26 | 10.0.0.67 |
| 30 | Marketing | 10.0.0.128/26 | 10.0.0.131 |
| 40 | Finance | 10.0.0.192/26 | 10.0.0.195 |

### WAN & Server Addressing

| Segment / Device | IP Address |
|---|---|
| Campus Transit Network | 10.11.11.0/24 |
| Router0 WAN Interface | 20.20.20.1/30 |
| Router2 WAN Interface | 20.20.20.2/30 |
| Router1 WAN Interface | 20.20.20.5/30 |
| Router3 WAN Interface | 20.20.20.6/30 |
| Green Network | 8.8.8.0/24 |
| Primary DHCP Server | 100.0.0.5 |
| Web Server 1 | 8.8.8.10 |
| Web Server 2 | 8.8.8.11 |
| Web Server 3 | 8.8.8.12 |

*Note: These addresses are used within an isolated simulation environment and are not intended as a production addressing plan.*

## 🔧 Troubleshooting Case Study: DHCP & Client Connectivity

One of the main challenges during this project was resolving DHCP and client connectivity issues.

### Identified Issues

During network inspection, several configuration problems were identified:

1. The primary DHCP server was connected to an access port assigned to the default VLAN instead of VLAN 100.
2. The VLAN 100 uplink between the data-center switch and the core network was missing.
3. A duplicate `100.0.0.1` SVI address was configured.
4. Some DHCP relay (`ip helper-address`) configurations were missing from the second core switch's VLAN interfaces.

### Troubleshooting & Resolution

The following actions were performed:

1. Corrected the DHCP server access port VLAN assignment.
2. Restored the VLAN 100 connectivity path.
3. Removed the duplicate SVI IP address while preserving the intended gateway.
4. Added the missing DHCP relay configurations.
5. Re-tested client addressing and end-to-end connectivity.


## 🧪 Testing & Validation

The following tests were documented during the project:

| Test | Result |
|---|---|
| Router0 to WAN peer (20.20.20.2) | 5/5 successful replies |
| OSPF WAN Neighbor | FULL/BDR |
| Internal OSPF Neighbors | Three FULL adjacencies observed |
| PC5 IP Configuration | Valid VLAN 10 addressing |
| PC5 to Web Server (8.8.8.12) | 4/4 successful replies |
| HTTP Access to 8.8.8.10 | Successfully loaded Packet Tracer default web page |





### Client Connectivity Tests

```bash
ipconfig
ping 10.0.0.3
ping 100.0.0.5
ping 8.8.8.10
ping 8.8.8.11
ping 8.8.8.12
```

### Router Verification Commands

Run these commands from the privileged EXEC mode (`#`):

```bash
show ip interface brief
show ip ospf neighbor
show ip route
ping 20.20.20.2
```

## 🎯 Skills Demonstrated

- Network Design & Topology Configuration
- IPv4 Addressing & Subnetting
- VLAN Configuration & Trunking
- Inter-VLAN Routing
- HSRP Configuration
- Multi-Area OSPF
- DHCP & DHCP Relay
- WAN Connectivity
- Layer 2 & Layer 3 Troubleshooting
- ICMP & HTTP Connectivity Testing
- Network Documentation



**Developed by Rana Yehia**

