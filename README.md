# CCNA-Network-Topology

A complete end-to-end multi-switch and multi-router enterprise network topology built in Cisco Packet Tracer to demonstrate hands-on Layer 2/3 network engineering, protocol design and CCNA (200-301) exam topics.

---

## Topology Architecture & Region Segmentation

To capture both enterprise scale and smaller site requirements, the network topology is split across two visual captures based on regional scale:

![Enterprise Region Topology Diagram](./images/Arizona%20Topology.png)
*Figure 1: Arizona Regional Hub Architecture*

![Branch Region Topology Diagram](./images/Fl,%20Nv%20Topology.png)
*Figure 2: Florida and Nevada Regional Architecture*

### Regional Breakdown & Scale Model
* **Arizona Region (Large Enterprise Model):** Functions as the primary enterprise regional hub.
* **Florida Region (Small Business Branch Model):** Modeled as a streamlined branch location.
* **Nevada Region (Small Business Branch Model):** Configured as a secondary branch location.

*Note: Specific topology adjustments and custom protocol configurations were made beyond the base CBT Nuggets model to test features and verify edge cases.*

---

## Lab Access & Credentials

To access and test device configurations across the topology, use the following credentials:

| Access Type / Device | Username | Password / PSK |
| :--- | :--- | :--- |
| **Console Access** | — | `cisco` |
| **Privileged EXEC Mode (`enable`)** | — | `cisco` |
| **SSH Session** | `Yexall` | `123` |
| **WLC Management GUI/CLI** | `Yexall` | `Cisco123` |
| **WLAN SSID (`NetworkNINJA`)** | — | `11223344` |

--- 

## Technical Highlights & Protocol Implementations

* **VLSM Subnetting & Addressing:** Calculated custom Variable Length Subnet Masks (VLSM) across LAN segments, maximizing IP space efficiency across discrete VLAN broadcast domains.
* **VLAN Segmentation & Trunk Negotiation:** Partitioned switch ports into functional VLANs (10, 20, 30, 40, 45) using 802.1Q trunk links, explicitly configuring Dynamic Trunking Protocol (DTP) modes to restrict unauthorized trunk negotiation.
* **VLAN Traffic Containment & Pruning:** Configured manual VLAN trunk pruning and access restrictions across intermediate switches to isolate broadcast domains and prevent unnecessary traffic flooding on uninvolved nodes.
* **Inter-VLAN Routing (All regions):** Implemented Layer 3 Inter-VLAN routing using Router-on-a-Stick subinterfaces on routers and integrated multilayer switch configurations via router EtherSwitch modules.
* **Spanning Tree Protocol (STP) Tuning:** Manipulated STP bridge priorities to explicitly designate Root Bridges and control designated/blocked port roles for deterministic Layer 2 loop prevention.
* **Topology Discovery & Path Verification:** Mapped physical inter-switch connections using Cisco Discovery Protocol (CDP) and Link Layer Discovery Protocol (LLDP) neighbor tables, explicitly enabling and disabling protocols globally or on specific interfaces to control neighbor updates, visibility and link path verification.
* **EtherChannel Aggregation & Load Balancing (Az):** Grouped physical interfaces into logical Port-Channels across inter-switch links and configured custom frame load-distribution algorithms to optimize traffic hashing and eliminate link congestion.
* **Enterprise Wireless LAN Deployment (Az):** Integrated a Wireless LAN Controller (WLC) and Lightweight Access Points (LAPs) to provide centralized wireless management, WPA2-PSK security and dynamic IP provisioning across dedicated wireless VLANs.
* **Static and Default Routing:** Configured explicit static routes on the MetroE router and default routes (`0.0.0.0/0`) on regional edge routers.
* **Hybrid NAT/PAT Strategy & Dynamic Pool Allocation (Az):** Implemented a dual-NAT architecture on the edge router using both Interface-based PAT for local VLANs and Dynamic NAT with Pool Overload across a public block for downstream subnets routed over the MetroE transit link.
* **Network Time Protocol (NTP) Hierarchy (All regions):** Established a complete hierarchical NTP design where the Arizona edge router pulls time from an external NTP server across the ISP router, acting as the primary enterprise time source. It then feeds the Florida and Nevada regional edge routers, which serve as local NTP masters for their respective branch switches and downstream devices.

--- 

## Verification & Commands Used

The integrity of the network topology was verified using key diagnostic commands:
* `show vlan brief` & `show interfaces trunk` — Verified VLAN membership and 802.1Q trunking parameters.
* `show cdp neighbors` / `show lldp neighbors` — Validated neighbor relationships and local/remote port mappings.
* `show spanning-tree` — Confirmed Root Bridge election and blocked/designated port states.
* `show etherchannel summary` & `show etherchannel load-balance` — Validated operational status of Port-Channels, member port bundling and load-distribution methods.
* `show ip route` — Validated active routing table entries and verified default gateway propagation.
* `show ip nat translations` & `show access-lists` — Verified active real-time NAT/PAT mappings while cross-referencing ACL match counters to ensure downstream subnet traffic correctly triggered translation rules.
* `show ntp status` & `show ntp associations` — Validated clock synchronization state, stratum levels and upstream/downstream peer associations.

---

## Troubleshooting Highlights

### Wireless LAN Controller (WLC) & AP Isolation
* **DHCP Scope Definitions:** Resolved subnet vs. host IP configuration issues by defining proper Subnet IDs (`10.16.0.0/24`) and Pool Start addresses (`10.16.0.11`).
* **Traffic Flow Validation:** Used static IP addressing (`10.16.0.50`) to isolate and verify CAPWAP tunnel encapsulation and bridge forwarding independently from DHCP relay behavior.
### Hybrid NAT/PAT & Downstream Routing (Az-R1 & MetroE)
* **Bidirectional Routing & Gateway of Last Resort:** Resolved issue where PCs behind the MetroE router could reach `Az-R1`'s LAN interface but failed to ping the public WAN gateway by configuring a default route on the MetroE router pointing back to `Az-R1`.
* **Private IP Pool Address Dropping:** Identified packet loss when testing dynamic pool translations using RFC 1918 private IP pools (`192.168.1.x`). Resolved by reallocating the pool to use valid public IP addresses (`203.0.113.x/29`) within the ISP's assigned range so return traffic could be routed properly across the WAN edge.

---

## To-Do List
- [ ] Az: Fix wireless laptop not receiving DHCP address due to lease timeout.
