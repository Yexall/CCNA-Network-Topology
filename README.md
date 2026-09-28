# CCNA-Network-Topology

A complete end-to-end multi-switch and multi-router enterprise network topology built in Cisco Packet Tracer to demonstrate hands-on Layer 2/3 network engineering, protocol design and CCNA (200-301) exam topics.

--- 

## Technical Highlights & Protocol Implementations

* **VLSM Subnetting & Addressing:** Calculated custom Variable Length Subnet Masks (VLSM) across LAN segments, maximizing IP space efficiency across discrete VLAN broadcast domains.
* **VLAN Segmentation & Trunk Negotiation:** Partitioned switch ports into functional VLANs (VLAN 10, VLAN 20, VLAN 30, VLAN 40, VLAN 45) using 802.1Q trunk links, explicitly configuring Dynamic Trunking Protocol (DTP) modes to restrict unauthorized trunk negotiation.
* **VLAN Traffic Containment & Pruning:** Configured manual VLAN trunk pruning and access restrictions across intermediate switches to isolate broadcast domains and prevent unnecessary traffic flooding on uninvolved nodes.
* **Inter-VLAN Routing:** Implemented Layer 3 Inter-VLAN routing using Router-on-a-Stick subinterfaces on routers and integrated multilayer switch configurations via router EtherSwitch modules.
* **Spanning Tree Protocol (STP) Tuning:** Manipulated STP bridge priorities to explicitly designate Root Bridges and control designated/blocked port roles for deterministic Layer 2 loop prevention.
* **Topology Discovery & Path Verification:** Utilized Cisco Discovery Protocol (CDP) and Link Layer Discovery Protocol (LLDP) neighbor tables to map physical interconnects and verify active link paths.

--- 

## Verification & Commands Used

The integrity of the network topology was verified using key diagnostic commands:
* `show vlan brief` & `show interfaces trunk` — Verified VLAN membership and 802.1Q trunking parameters.
* `show cdp neighbors` / `show lldp neighbors` — Validated neighbor relationships and local/remote port mappings.
* `show spanning-tree` — Confirmed Root Bridge election and blocked/designated port states.
