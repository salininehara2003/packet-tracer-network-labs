# Enterprise Switched Network: VLANs, VTP, Inter-VLAN Routing, EtherChannel & STP

## Project Overview
This Cisco Packet Tracer lab demonstrates the design, configuration, and verification of a multi-switch enterprise campus network. It integrates Layer 2 switching redundancy, link aggregation, centralized VLAN management, and Layer 3 inter-VLAN routing using a multilayer switch.

## Network Architecture & Devices
* **Core / Distribution Layer:** 1x Cisco Catalyst 3560-24PS Multilayer Switch (VTP Server & Inter-VLAN Router)
* **Access Layer:** 3x Cisco Catalyst 2960-24TT Switches (VTP Clients)
* **End Devices:** 7x Host PCs segmented across 3 logical VLANs (`VLAN 10`, `VLAN 20`, and `VLAN 30`)

## IP Addressing & VLAN Scheme
| VLAN ID | Subnet | Default Gateway (SVI) | Assigned Hosts (IP Addresses) |
| :--- | :--- | :--- | :--- |
| **VLAN 10** | `192.168.10.0/24` | `192.168.10.1` | `192.168.10.10`, `192.168.10.11` |
| **VLAN 20** | `192.168.20.0/24` | `192.168.20.1` | `192.168.20.10`, `192.168.20.11` |
| **VLAN 30** | `192.168.30.0/24` | `192.168.30.1` | `192.168.30.10`, `192.168.30.11`, `192.168.30.12` |

## Key Features & Configurations Implemented
1. **VLAN Segmentation:**
   * Created VLAN 10, VLAN 20, and VLAN 30 to isolate broadcast domains.
   * Configured access ports on the 2960 switches and assigned end-host interfaces to their respective VLANs.
2. **VLAN Trunking Protocol (VTP):**
   * Configured the 3560 Multilayer Switch as the **VTP Server** and the 2960 access switches as **VTP Clients** under a consistent VTP domain and password.
   * Configured 802.1Q trunk links between switches to propagate VLAN databases automatically.
3. **LACP Link Aggregation (EtherChannel):**
   * Bundled redundant physical FastEthernet links between switches into logical Port-Channel interfaces using **LACP** (`active` / `passive` modes) to increase bandwidth and provide link-level fault tolerance.
4. **Inter-VLAN Routing via SVIs:**
   * Enabled IPv4 routing (`ip routing`) on the 3560 Multilayer Switch.
   * Configured Switched Virtual Interfaces (`interface vlan 10`, `20`, and `30`) to act as default gateways, enabling seamless Layer 3 communication between different VLANs.
5. **Spanning Tree Protocol (STP):**
   * Verified PVST+ operation, root bridge election, and port states across the redundant looped topology.
   * Tested link failover scenarios to ensure loop-free convergence without dropping end-to-end connectivity.

## Verification & Testing
* **VTP & VLAN Propagation:** Verified using `show vtp status` and `show vlan brief` across all switches.
* **EtherChannel Bundling:** Confirmed active port-channel states (`SU` / `P`) using `show etherchannel summary` and tested single-link disconnection resilience.
* **STP Convergence:** Inspected root bridge roles and blocking/forwarding states via `show spanning-tree`.
* **End-to-End Connectivity:** Verified intra-VLAN and inter-VLAN reachability using ICMP `ping` tests across all subnets.

## Files Included
* `Practice_TakeHomeLab_DN.pkt` — Completed Cisco Packet Tracer simulation file.
* `Topology.png` — Visual diagram of the network architecture and interface mappings.
