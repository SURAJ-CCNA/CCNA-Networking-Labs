# Inter-VLAN Routing & Extended ACL Security Lab

*Cisco Packet Tracer Enterprise Network Implementation & Security Hardening*

## 📌 Project Overview

This project demonstrates enterprise network segmentation using VLANs, Router-on-a-Stick, subnetting, and Extended Access Control Lists (ACLs) in Cisco Packet Tracer. The topology represents a multi-department campus network with isolated departmental VLANs, centralized servers, and security policies.

## 📐 Network Topology & Subnet Allocation Matrix

| VLAN ID | Department / Name | Network Subnet | Gateway IP | Allocation Purpose |
|---|---|---|---|---|
| 10 | SALES | `192.168.10.0/24` | `192.168.10.1` | Sales workstations and laptops |
| 20 | HR | `192.168.20.0/24` | `192.168.20.1` | Human Resources workstations |
| 30 | IT | `192.168.30.0/24` | `192.168.30.1` | IT department and administration |
| 40 | FINANCE | `192.168.40.0/24` | `192.168.40.1` | Finance and accounting department |
| 50 | CANTEEN | `192.168.50.0/24` | `192.168.50.1` | Public/canteen network segment |
| 60 | ENTC (Server) | `192.168.60.0/24` | `192.168.60.1` | ENTC department and Server0 |
| 70 | CSE | `192.168.70.0/24` | `192.168.70.1` | Computer Science Engineering lab |
| 80 | MECH (Server) | `192.168.80.0/24` | `192.168.80.1` | Mechanical lab and Server1 |
| Transit | ROUTER-LINK | `10.10.10.0/30` | `10.10.10.1` / `10.10.10.2` | Point-to-point router backbone link |

## 🧠 Core Architecture & Device Functions

1. **Routers (`Router0` and `Router1`):** Provide inter-network routing and backbone connectivity. Router-on-a-Stick uses IEEE 802.1Q subinterfaces to route traffic between VLANs when configured on the appropriate router interface.
2. **Access Switches (`Switch0`, `Switch1`, `Switch2`):** Cisco Catalyst 2950/2960 switches provide end-device connectivity and VLAN trunking toward upstream devices.
3. **Enterprise Servers:** Server0 belongs to VLAN 60, and Server1 belongs to VLAN 80. They represent centralized application and data services.

## 🛡️ Extended ACL Security Policy (`CORP-SECURITY`)

The following example ACL defines traffic policies for the enterprise network.

```cisco
ip access-list extended CORP-SECURITY
 ! Rule 1: Permit IT Department (VLAN 30) to access any destination
 permit ip 192.168.30.0 0.0.0.255 any

 ! Rule 2: Permit Finance (VLAN 40) to access the ENTC server subnet
 permit ip 192.168.40.0 0.0.0.255 192.168.60.0 0.0.0.255

 ! Rule 3: Deny Sales (VLAN 10) access to the MECH server subnet
 deny ip 192.168.10.0 0.0.0.255 192.168.80.0 0.0.0.255

 ! Rule 4: Permit all other IP traffic
 permit ip any any
```

**Important:** ACL rules are processed from top to bottom, and the first matching rule applies. The final `permit ip any any` permits other IP traffic not matched by an earlier rule. Apply the ACL to the correct routed interface and direction based on the intended traffic flow.

## ⚙️ Core Router Configuration Snippets

### 1. Router-on-a-Stick Configuration (`Router0`)

The following example configures VLAN 10 and VLAN 30 subinterfaces. Repeat the pattern for the remaining VLANs as required by the topology.

```cisco
enable
configure terminal

interface GigabitEthernet0/1
 no shutdown
 exit

! VLAN 10 - SALES
interface GigabitEthernet0/1.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 exit

! VLAN 30 - IT
interface GigabitEthernet0/1.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
 exit
```

### 2. Applying the Extended ACL

```cisco
configure terminal
interface GigabitEthernet0/1
 ip access-group CORP-SECURITY in
 exit

end
write memory
```

**Note:** This is a configuration template, not a complete configuration for all eight VLANs. Confirm the actual interface names and ensure each VLAN has a correctly configured gateway and switch trunk. The ACL must also be applied at a point where it can inspect the traffic it is intended to control.

## 🚀 Testing & Verification in Cisco Packet Tracer

After completing and verifying the configurations, perform these tests:

- **IT Access:** From PC2 in VLAN 30, ping Server0 in VLAN 60 or Server1 in VLAN 80. Expected: success, provided routing and server settings are correct.
- **Finance Access:** From PC3 in VLAN 40, ping Server0 in VLAN 60. Expected: success, provided routing and server settings are correct.
- **Sales Restriction:** From PC0 or Laptop0 in VLAN 10, ping Server1 in VLAN 80. Expected: blocked by ACL Rule 3, provided the ACL is applied on the correct interface and direction.
- **ACL Hit Counters:** Run `show access-lists` on the router to inspect rule match counters.
- **Interface Status:** Run `show ip interface brief` to verify that the relevant interfaces are operational.

## 📚 Skills Demonstrated

- VLAN segmentation and subnet planning
- IEEE 802.1Q trunking
- Router-on-a-Stick configuration
- Extended ACL configuration and traffic filtering
- Router and switch troubleshooting
- Connectivity testing and ACL verification

## 🛠️ Tools & Technologies

- Cisco Packet Tracer
- Cisco IOS CLI
- VLANs and trunking
- IPv4 subnetting
- Extended Access Control Lists (ACLs)

