# CCNA-Network-Topology

A complete end-to-end multi-switch and multi-router enterprise network topology built in Cisco Packet Tracer to demonstrate hands-on Layer 2/3 network engineering, protocol design and CCNA (200-301) exam topics.

---

## Topology Architecture & Region Segmentation

To capture both enterprise scale and smaller site requirements, the network topology is split across two visual captures based on regional scale:

![Enterprise Region Topology Diagram](./Images/Arizona%20Topology.png)
*Figure 1: Arizona Regional Hub Architecture*

![Branch Region Topology Diagram](./Images/Fl,%20Nv%20Topology.png)
*Figure 2: Florida and Nevada Regional Architecture*

### Regional Breakdown & Scale Model
* **Arizona Region (Large Enterprise Model):** Functions as the primary enterprise regional hub.
* **Florida Region (Small Business Branch Model):** Modeled as a streamlined branch location.
* **Nevada Region (Small Business Branch Model):** Configured as a secondary branch location.

*Note: Specific topology adjustments and custom protocol configurations were made beyond the base CBT Nuggets model to test features and verify edge cases.*

--- 

## Technical Highlights & Protocol Implementations

* **VLSM Subnetting & Addressing:** Calculated custom Variable Length Subnet Masks (VLSM) across LAN segments, maximizing IP space efficiency across discrete VLAN broadcast domains.
* **VLAN Segmentation & Trunk Negotiation:** Partitioned switch ports into functional VLANs (10, 20, 30, 40, 45) using 802.1Q trunk links, explicitly configuring Dynamic Trunking Protocol (DTP) modes to restrict unauthorized trunk negotiation.
* **VLAN Traffic Containment & Pruning:** Configured manual VLAN trunk pruning and access restrictions across intermediate switches to isolate broadcast domains and prevent unnecessary traffic flooding on uninvolved nodes.
* **Inter-VLAN Routing:** Implemented Layer 3 Inter-VLAN routing using Router-on-a-Stick subinterfaces on routers and integrated multilayer switch configurations via router EtherSwitch modules.
* **Spanning Tree Protocol (STP) Tuning:** Manipulated STP bridge priorities to explicitly designate Root Bridges and control designated/blocked port roles for deterministic Layer 2 loop prevention.
* **Topology Discovery & Path Verification:** Mapped physical inter-switch connections using Cisco Discovery Protocol (CDP) and Link Layer Discovery Protocol (LLDP) neighbor tables, explicitly enabling and disabling protocols globally or on specific interfaces to control neighbor updates, visibility and link path verification.

--- 

## Verification & Commands Used

The integrity of the network topology was verified using key diagnostic commands:
* `show vlan brief` & `show interfaces trunk` — Verified VLAN membership and 802.1Q trunking parameters.
* `show cdp neighbors` / `show lldp neighbors` — Validated neighbor relationships and local/remote port mappings.
* `show spanning-tree` — Confirmed Root Bridge election and blocked/designated port states.
