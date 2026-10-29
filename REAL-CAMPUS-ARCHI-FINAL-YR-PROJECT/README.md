# Enterprise Secure Campus Network Architecture & Implementation

**A B.Tech Final-Year Capstone Project in Computer Science and Engineering (Cybersecurity Honors)**

## 📌 Project Overview

This repository documents the design, simulation, configuration, and troubleshooting of an **Enterprise Secure Campus Network** built using Cisco Packet Tracer.

The architecture simulates a multi-department academic and administrative network with hierarchical switching, inter-VLAN routing, centralized server services, and network access control using Extended Access Control Lists (ACLs).

## 📐 Enterprise Network Topology & Architecture

The campus network follows a hierarchical network design model.

### 1. Access Layer — Cisco Catalyst 2960 Switches
- Provides end-device connectivity across 11 computer laboratories.
- Supports VLAN-based network segmentation and 802.1Q trunk uplinks.
- Supports Spanning Tree Protocol (STP) for Layer 2 loop prevention.
- Port security can be implemented to restrict unauthorized device access.

### 2. Distribution and Core Layer — Cisco Catalyst 3560 Multilayer Switch
- Performs Layer 3 routing between VLANs.
- Uses Switched Virtual Interfaces (SVIs) as default gateways.
- Provides connectivity between laboratory networks and the server network.
- Supports centralized routing and network segmentation.

### 3. Enterprise Edge and Server Farm
- **Cisco 2911 Router:** Provides routed connectivity and can enforce perimeter ACL policies.
- **VLAN 30 — Server Farm:** Hosts centralized network services.
- **Extended ACLs:** Restrict traffic according to source, destination, and protocol.

## 🗂️ Master VLAN & IP Allocation Matrix

| VLAN ID | VLAN / Lab Name | Network Subnet | Gateway IP (SVI) | Usable Host Range | Purpose |
|---|---|---|---|---|---|
| 10 | LAB01-HNL | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.2–192.168.10.254 | Hardware & Networking Lab |
| 11 | LAB02-PROJECT | 192.168.11.0/24 | 192.168.11.1 | 192.168.11.2–192.168.11.254 | Project Development Lab 02 |
| 12 | LAB03-OS | 192.168.12.0/24 | 192.168.12.1 | 192.168.12.2–192.168.12.254 | Operating Systems Lab |
| 13 | LAB04-PROJECT | 192.168.13.0/24 | 192.168.13.1 | 192.168.13.2–192.168.13.254 | Project Development Lab 04 |
| 14 | CC-CENTER-1 | 192.168.14.0/24 | 192.168.14.1 | 192.168.14.2–192.168.14.254 | Computer Center Block 1 |
| 15 | CC-CENTER-2 | 192.168.15.0/24 | 192.168.15.1 | 192.168.15.2–192.168.15.254 | Computer Center Block 2 |
| 16 | CC-CENTER-3 | 192.168.16.0/24 | 192.168.16.1 | 192.168.16.2–192.168.16.254 | Computer Center Block 3 |
| 17 | CC-CENTER-4 | 192.168.17.0/24 | 192.168.17.1 | 192.168.17.2–192.168.17.254 | Computer Center Block 4 |
| 18 | LAB05-PROJECT | 192.168.18.0/24 | 192.168.18.1 | 192.168.18.2–192.168.18.254 | East Wing Project Lab 01 |
| 19 | LAB06-DATABASE | 192.168.19.0/24 | 192.168.19.1 | 192.168.19.2–192.168.19.254 | Database & Analytics Lab |
| 20 | LAB07-EASTWING | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.2–192.168.20.254 | East Wing General Computer Lab |
| 30 | SERVER-FARM | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.2–192.168.30.254 | Centralized Network Services |
| 90 | ADMIN-FACULTY | 192.168.90.0/24 | 192.168.90.1 | 192.168.90.2–192.168.90.254 | Faculty & Administration |
| — | L3-ROUTER-LINK | 10.0.0.0/30 | 10.0.0.1 (L3 Switch) | 10.0.0.1–10.0.0.2 | Point-to-Point Link |

**Note:** The usable host range for the `/30` transit subnet is `10.0.0.1–10.0.0.2`; the network address is `10.0.0.0` and the broadcast address is `10.0.0.3`.

## 🧠 Network Device Roles

| Device | Primary Role |
|---|---|
| Cisco 2911 Router | Routed connectivity and perimeter ACL enforcement |
| Cisco 3560 Multilayer Switch | Inter-VLAN routing and SVI gateways |
| Cisco 2960 Access Switches | End-device connectivity and VLAN-aware switching |
| Centralized Servers | Network services, file transfer, and event logging |

## 🖥️ Centralized Server Allocation

The following addresses are the planned server assignments within VLAN 30.

| Service | IP Address | Protocol / Port |
|---|---|---|
| DNS | 192.168.30.2 | UDP/TCP 53 |
| Syslog | 192.168.30.3 | UDP 514 |
| TFTP | 192.168.30.4 | UDP 69 |
| DHCP | 192.168.30.5 | UDP 67/68 |
| FTP | 192.168.30.6 | TCP 20/21 |

## 🔌 Protocols and Their Roles

- **IEEE 802.1Q:** Carries traffic for multiple VLANs across a trunk link using VLAN tags.
- **Inter-VLAN Routing:** Enables communication between VLANs according to Layer 3 routing and security policies.
- **DHCP Relay:** Uses `ip helper-address` to forward DHCP requests from remote VLANs to a centralized DHCP server.
- **DNS:** Resolves hostnames into IP addresses.
- **TFTP:** Provides lightweight file transfer, including potential configuration backup and recovery workflows.
- **Syslog:** Centralizes network device event messages.
- **FTP:** Supports file transfers between clients and the designated server.

## 🛡️ Extended ACL Security Design

The following named Extended ACL illustrates the intended traffic policy for the administration network and TFTP server.

```cisco
ip access-list extended secure-labs
 10 permit ip 192.168.90.0 0.0.0.255 any
 20 permit tcp any 192.168.90.0 0.0.0.255 established
 30 permit icmp any 192.168.90.0 0.0.0.255 echo-reply
 40 deny ip any 192.168.90.0 0.0.0.255
 50 deny ip any host 192.168.30.4
 60 permit ip any any
```

### ACL Rule Explanation

- **Rule 10:** Permits traffic originating from the administration subnet.
- **Rule 20:** Permits matching TCP packets with the ACK or RST flag set toward the administration subnet. This is not full stateful inspection.
- **Rule 30:** Permits ICMP echo-reply traffic toward the administration subnet.
- **Rule 40:** Denies other IP traffic toward the administration subnet.
- **Rule 50:** Denies traffic to the TFTP server.
- **Rule 60:** Permits other IP traffic not matched by earlier rules.

**Important:** ACLs are processed from top to bottom, and the first matching rule applies. Because rule 60 permits all other IP traffic, this policy is not a complete Zero-Trust design. Rule ordering, interface direction, and actual traffic requirements must be reviewed and tested before deployment. The `established` keyword is not equivalent to a stateful firewall.

## ⚙️ Core Device Configuration Examples

### Multilayer Switch — Initial Configuration

```cisco
enable
configure terminal

ip routing

interface Vlan10
 description GATEWAY-LAB01-HNL
 ip address 192.168.10.1 255.255.255.0
 ip helper-address 192.168.30.5
 no shutdown
exit

interface GigabitEthernet0/1
 no switchport
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit

ip route 0.0.0.0 0.0.0.0 10.0.0.2
ip route 192.168.30.0 255.255.255.0 10.0.0.2

logging 192.168.30.3

end
write memory
```

**Note:** Configure the remaining SVIs and DHCP relay addresses as required. The sample above shows VLAN 10 only. Ensure the transit interface name and available commands match the Packet Tracer device model.

### Edge Router — Example Static Route

```cisco
enable
configure terminal

ip route 192.168.10.0 255.255.255.0 10.0.0.1

end
write memory
```

Add routes for the other VLAN subnets as needed. Apply the `secure-labs` ACL to the correct interface and direction only after verifying the intended traffic flow.

## 🧪 Verification and Troubleshooting

Use the following commands where supported by the device:

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show access-lists
show running-config
```

Test connectivity with `ping` and `traceroute`. Verify both permitted and denied traffic, VLAN membership, trunk status, SVI state, and routing-table entries.

## 📁 Repository Contents

Add your actual project files to the repository:

- Cisco Packet Tracer simulation (`.pkt`)
- Network topology diagram
- VLAN and IP addressing tables
- Device configuration files
- Verification screenshots
- Troubleshooting documentation

## 🎯 Learning Outcomes

- Enterprise network architecture and hierarchical design
- VLAN segmentation and trunking
- Inter-VLAN routing using Layer 3 switching
- IPv4 subnetting and addressing
- Extended ACL configuration and traffic filtering
- Centralized network services
- Cisco IOS configuration and troubleshooting

## 🚀 Future Enhancements

- Complete and document OSPF routing.
- Expand ACL policies and test isolation between departments.
- Implement port security and secure device management using SSH.
- Validate centralized DHCP, DNS, TFTP, Syslog, and FTP services.
- Add network monitoring and configuration backup workflows.

---

**Project Title:** Enterprise Secure Campus Network Architecture & Implementation  
**Project Type:** B.Tech Final-Year Capstone Project  
**Domain:** Computer Networking and Cybersecurity  
**Simulation Platform:** Cisco Packet Tracer  

**Developed by Suraj Bedekar**  
B.Tech Computer Science and Engineering — Cybersecurity Honors
