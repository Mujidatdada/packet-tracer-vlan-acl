# Cisco Packet Tracer Lab: VLANs, Inter-VLAN Routing & ACLs

## Overview

This project was created as part of my AltSchool exam to demonstrate core networking concepts using Cisco Packet Tracer. It covers:

- **VLAN segmentation** for structured traffic flow
- **Inter-VLAN Routing** using Router-on-a-Stick (ROAS)
- **Access Control Lists (ACLs)** to implement traffic restrictions
- **Connectivity testing** via ping, traceroute, and Wireshark

---

## 1. VLAN Configuration

To segment the network, three VLANs were created:

- **VLAN 10** – HR
- **VLAN 20** – Finance

### Sub-interface Configuration

```bash
Router> enable
Router# configure terminal

Router(config)# interface GigabitEthernet 0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface GigabitEthernet 0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

**After configuring the sub-interfaces, Inter-VLAN communication became possible.
**
2. ACL Implementation for Security
To restrict traffic between VLANs, I applied a standard access control policy:

```bash
Router(config)# access-list 100 deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
Router(config)# access-list 100 permit ip any any

Router(config)# interface GigabitEthernet 0/0
Router(config-if)# ip access-group 100 in
Router(config-if)# exit
✅ This configuration blocks traffic from VLAN 10 to VLAN 20 but allows all other communication.

3. Connectivity Testing & Results
Tools Used:
Ping – to verify reachability

Traceroute – to analyze path

Wireshark – to inspect packet-level communication

Key Observations:
Before Inter-VLAN Routing: No cross-VLAN communication.

After Sub-interface Setup: VLANs could communicate.

After ACLs: Access control enforced as expected.

4. Files Included
vlan-acl-config.pkt: Main Cisco Packet Tracer file

README.md: Project documentation

Conclusion
This project strengthened my understanding of:

VLAN segmentation for better network design

Router-on-a-Stick (ROAS) configuration

Real-world application of ACLs for securing traffic

It serves as a practical demonstration of how to manage, secure, and troubleshoot segmented networks in enterprise environments.

Author
Mujidat Dada – Cybersecurity Student at AltSchool Africa
