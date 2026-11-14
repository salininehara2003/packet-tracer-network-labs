# VLANs, VTP, Inter-VLAN Routing, EtherChannel & STP

## Project Overview

This project demonstrates the design, configuration, and verification of a switched network using Cisco Packet Tracer.

The network consists of one multilayer switch, three Cisco 2960 access switches, and end-user PCs distributed across multiple VLANs.

The multilayer switch operates as the central network device, providing VLAN management through VTP, inter-VLAN routing using Switched Virtual Interfaces (SVIs), and redundant connectivity through EtherChannel links.

The project also demonstrates how Spanning Tree Protocol (STP) prevents Layer 2 switching loops and maintains network stability.

## Network Topology

The network topology consists of:

- 1 Multilayer Switch (Cisco 3560)
- 3 Access Switches (Cisco 2960)
- 6 end-user PCs (as shown in the topology diagram)
- Multiple redundant inter-switch connections

### Network Architecture

The multilayer switch acts as the central switch and VTP Server. The three access switches connect end-user devices and operate as VTP Clients.

Redundant links between switches are configured using LACP EtherChannel to improve link availability and bandwidth utilization.

## VLAN and IP Addressing

Three VLANs are configured to logically separate network devices.

| VLAN ID | VLAN Name | Network Address |
|---|---|---|
| 10 | VLAN10 | 192.168.10.0/24 |
| 20 | VLAN20 | 192.168.20.0/24 |
| 30 | VLAN30 | 192.168.30.0/24 |

### Default Gateway Configuration

The multilayer switch provides the default gateways through SVIs.

| VLAN | SVI Address |
|---|---|
| VLAN 10 | 192.168.10.1 |
| VLAN 20 | 192.168.20.1 |
| VLAN 30 | 192.168.30.1 |

Subnet mask: `255.255.255.0`

## Technologies and Concepts Implemented

### 1. VLAN Configuration

- Created VLAN 10, VLAN 20, and VLAN 30.
- Assigned appropriate access ports to each VLAN.
- Verified VLAN membership using `show vlan brief`.

### 2. VLAN Trunking Protocol (VTP)

- Configured the multilayer switch as the VTP Server.
- Configured three access switches as VTP Clients.
- Configured a consistent VTP domain, version, and password.
- Established trunk links to propagate VLAN information.
- Verified VLAN propagation across the switches.

### 3. LACP EtherChannel

Configured four separate EtherChannels between switch pairs using LACP.

| Port Channel | Connected Switches |
|---|---|
| Po1 | Multilayer Switch ↔ SW0 |
| Po2 | Multilayer Switch ↔ SW2 |
| Po3 | SW0 ↔ SW1 |
| Po4 | SW1 ↔ SW2 |

- Configured physical member interfaces.
- Created logical Port-Channel interfaces.
- Verified EtherChannel operation using `show etherchannel summary`.
- Tested connectivity after disconnecting one physical member link.

### 4. Inter-VLAN Routing Using SVIs

- Created an SVI for each VLAN on the multilayer switch.
- Assigned IP addresses to the SVIs as default gateways.
- Enabled Layer 3 routing using `ip routing`.
- Enabled communication between devices belonging to different VLANs.

### 5. Spanning Tree Protocol (STP)

- Verified STP operation on all participating switches.
- Identified Switch0 as the Root Bridge.
- Examined root bridge election based on Bridge ID.
- Observed STP topology and port-state changes after disconnecting a link.

## Testing and Verification

The following tests and verification activities were performed:

| Test | Verification Method | Result |
|---|---|---|
| VLAN creation | `show vlan brief` | Verified |
| VTP propagation | VLAN database on client switches | Verified |
| Trunk configuration | `show interfaces trunk` | Verified |
| EtherChannel operation | `show etherchannel summary` | Verified |
| Same-VLAN communication | ICMP Ping | Successful |
| Inter-VLAN communication | ICMP Ping | Successful |
| EtherChannel link failure | Disconnect one member link and test connectivity | Communication maintained |
| STP operation | `show spanning-tree` | Verified |
| STP topology change | Disconnect a network link | Observed |

### EtherChannel Redundancy Test

One physical member link was disconnected from an operational EtherChannel.

The Port-Channel remained operational through the remaining physical link, and communication between devices continued.

This demonstrates the redundancy benefit of EtherChannel.

### Inter-VLAN Connectivity Test

Communication was tested between PCs belonging to different VLANs.

The multilayer switch successfully forwarded traffic between VLANs using the configured SVIs.

## Important Cisco IOS Commands

Some of the commands used during implementation and verification:

```bash
show vlan brief
show vtp status
show interfaces trunk
show etherchannel summary
show spanning-tree
show ip interface brief
show ip route
show running-config
```

## Tools Used

- Cisco Packet Tracer
- Cisco IOS Command-Line Interface (CLI)
- ICMP Ping for connectivity testing

## Learning Outcomes

Through this project, I gained practical experience in:

- Implementing VLAN-based network segmentation.
- Managing VLANs using VTP.
- Configuring trunk links between switches.
- Implementing link aggregation using LACP.
- Configuring inter-VLAN routing using SVIs.
- Understanding STP root bridge election and loop prevention.
- Testing network redundancy and troubleshooting connectivity.

## Project File

The Cisco Packet Tracer project file (`.pkt`) is included in this repository.

Download the file and open it using Cisco Packet Tracer to explore the network topology and configurations.

---
