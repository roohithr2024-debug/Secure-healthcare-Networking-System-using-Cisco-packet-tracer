# Secure Healthcare Information Network System

> An enterprise-grade hospital network designed and implemented in Cisco Packet Tracer — covering hierarchical design, VLANs, routing, VoIP, wireless, firewall security, and high availability.

---

## What It Does

Healthcare institutions require a robust, secure, and highly available network to support clinical operations, administrative workflows, patient communication, and emergency services. This project simulates a full-scale hospital network infrastructure using industry-standard Cisco technologies — from layer 2 switching all the way up to firewall zones, NAT, and wireless LAN controllers — all built and verified inside Cisco Packet Tracer.

Built with *Cisco IOS CLI* on multilayer switches, routers, ASA firewall, Wireless LAN Controller (WLC), and lightweight access points.

---

## Features

* Hierarchical network design (Core → Distribution → Access layers)
* VLAN segmentation for all hospital departments
* Inter-VLAN Routing via *SVI (Switch Virtual Interface)* and *Router-on-a-Stick*
* *OSPF* dynamic routing for internal network communication
* *HSRP* (Hot Standby Router Protocol) for gateway redundancy and high availability
* *EtherChannel (LACP)* for link aggregation between switches
* *STP PortFast & BPDUguard* on all access ports
* *DHCP Server* — automatic IP assignment per department VLAN
* *SSH* — secure remote device management (Telnet disabled)
* *Cisco ASA Firewall* — basic levels & zones, NAT, default route, and inspection policy
* *Standard & Extended ACLs* — traffic filtering and access control
* *VoIP* — voice communication via IP phones on dedicated Voice Gateway routers
* *Wireless LAN Controller (WLC)* with Lightweight Access Points (LWAPs)
* *Wireless Network* — secure staff and guest Wi-Fi
* Static IPv4 addressing for servers and infrastructure devices
* Full subnetting across all departments and segments

---

## Network Topology Overview


                          [ISP / Internet]
                                 |
                          [ASA Firewall]
                        (Zones: Outside | DMZ | Inside)
                                 |
                    .────────────┴────────────.
               [Core Router 1]          [Core Router 2]
                    │        HSRP            │
               [Multilayer Switch - Distribution]
             .───────────┼────────────.
        [Access SW 1] [Access SW 2] [Access SW 3]
             |              |              |
        [VLAN 10]      [VLAN 20]      [VLAN 30]
        Doctors        Nurses         Admin

        [Voice GW]   [WLC + APs]   [DHCP/DNS Server]


---

## VLAN & IP Addressing Plan

| VLAN ID | Department       | Network Address  | Default Gateway |
|---------|------------------|------------------|-----------------|
| 10      | Doctors          | 192.168.10.0/24  | 192.168.10.1    |
| 20      | Nurses           | 192.168.20.0/24  | 192.168.20.1    |
| 30      | Admin            | 192.168.30.0/24  | 192.168.30.1    |
| 40      | IT / Server Room | 192.168.40.0/24  | 192.168.40.1    |
| 50      | Management       | 192.168.50.0/24  | 192.168.50.1    |
| 60      | VoIP             | 192.168.60.0/24  | 192.168.60.1    |
| 70      | Wireless         | 192.168.70.0/24  | 192.168.70.1    |
| 80      | DMZ              | 192.168.80.0/24  | 192.168.80.1    |

---

## Technologies Implemented

| Category         | Technology                                              |
|------------------|---------------------------------------------------------|
| Network Design   | Hierarchical (Core / Distribution / Access)             |
| Switching        | VLANs, 802.1Q Trunking, STP PortFast, BPDUguard         |
| Routing          | OSPF, Inter-VLAN Routing (SVI + Router-on-a-Stick)      |
| High Availability| HSRP, EtherChannel (LACP)                               |
| Security         | Cisco ASA Firewall, ACLs (Standard & Extended), SSH     |
| Firewall         | Zones & Levels, NAT, Default Route, Inspection Policy   |
| Services         | DHCP Server, DNS                                        |
| VoIP             | IP Phones, Voice Gateway Router, Voice VLAN             |
| Wireless         | WLC, Lightweight Access Points (LWAP), Secure WLAN      |
| Addressing       | Subnetting, Static IPv4 for servers and infrastructure  |

---

## Firewall Configuration Summary

The Cisco ASA Firewall divides the network into three security zones:

| Zone    | Security Level | Segment                             |
|---------|---------------|--------------------------------------|
| Outside | 0             | Internet / ISP                       |
| DMZ     | 50            | Public-facing servers (web, email)   |
| Inside  | 100           | All internal hospital departments    |

Key configurations applied:
- NAT/PAT for internal hosts accessing the internet
- Default route pointing to ISP
- Inspection policy for stateful traffic filtering
- ACLs restricting inbound traffic to DMZ services only

---

## How It Works

Each hospital department is assigned a dedicated VLAN to isolate broadcast domains. Multilayer switches handle inter-VLAN routing internally via SVIs, while routers handle external routing through OSPF. HSRP ensures that if one core router fails, the standby router takes over seamlessly, preventing downtime. EtherChannel bundles multiple physical links between switches for increased bandwidth and redundancy.

VoIP phones register to the Voice Gateway router using a separate voice VLAN, ensuring QoS prioritization for call traffic. The WLC centrally manages all lightweight access points, providing unified wireless policy enforcement across the hospital. The ASA firewall sits at the perimeter, applying NAT for outbound traffic and enforcing inspection policies for all incoming connections.

Packet Tracer's simulation mode is used to trace and verify that each packet follows the correct path, and that ACLs and firewall rules block unauthorized access at the right points.

---

## Getting Started

### Requirements

* Cisco Packet Tracer *8.0 or higher*

### Opening the Project


1. Download secure_healthcare111.pkt from this repository
2. Open Cisco Packet Tracer
3. File → Open → select the .pkt file
4. Use Realtime Mode to explore the full topology
5. Switch to Simulation Mode to trace and test packet flows


### Testing Connectivity


# From any department PC — open the Command Prompt:

ping 192.168.10.1        # Test default gateway (Doctors VLAN)
ping 192.168.40.10       # Test server room reachability
ping 8.8.8.8             # Test internet access via NAT

# Test SSH to a router or switch:
ssh -l admin 192.168.50.1


---


## Concepts Demonstrated

This project is a practical implementation of core Computer Networks and Network Security topics:

* *Network Layer* — IP addressing, subnetting, OSPF dynamic routing
* *Data Link Layer* — VLANs, 802.1Q trunking, EtherChannel (LACP), STP
* *Transport & Application Layer* — DHCP, DNS, SSH, VoIP (SIP/RTP)
* *Security* — ASA Firewall zones, NAT, ACLs, BPDUguard, SSH hardening
* *Wireless* — WLC + LWAP centralized architecture, SSID configuration
* *High Availability* — HSRP gateway failover, redundant uplinks

---


## Academic Context

* *Subject:* Computer Networks / Network Security
* *Institution:* Vellore Institute of Technology, Chennai

### Developed By

| Name |
|------|
| Roohith R |
| Lakkshanth R |

*Project Guide:* Prof. Swaminathan Annadurai

---



Output implementation:
<img width="1358" height="797" alt="image" src="https://github.com/user-attachments/assets/5edb43a7-ea5a-40ad-a9eb-d4a101b4ec32" />

<img width="1919" height="827" alt="image" src="https://github.com/user-attachments/assets/9e397b0c-5d1b-45b5-9e27-7a00023d4691" />

## License

This project is developed for academic and educational purposes.
