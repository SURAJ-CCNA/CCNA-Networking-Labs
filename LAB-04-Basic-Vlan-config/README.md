# VLAN Configuration Project (Cisco Packet Tracer)

## 📌 Overview
This project demonstrates a basic **Router-on-a-Stick** setup used to enable communication between multiple VLANs using a single router and a Layer 2 switch. It was built and tested in **Cisco Packet Tracer**.

## 🎯 Objective
- Segment a network into multiple VLANs for better organization, security, and traffic control.
- Configure inter-VLAN routing using **sub-interfaces** on a single router link (Router-on-a-Stick method).
- Verify connectivity between devices in different VLANs.

## 🖧 Network Topology

| Device | Role |
|--------|------|
| R1 | Router — performs inter-VLAN routing |
| SW | Layer 2 Switch — assigns VLANs to access ports |
| PC1, PC2 | End devices in VLAN 10 |
| PC3, PC4 | End devices in VLAN 20 |
| PC5, PC6 | End devices in VLAN 30 |

## 🗂️ VLAN Design

| VLAN ID | Name | Subnet | Gateway | Hosts |
|---------|------|--------|---------|-------|
| 10 | Engineering | 10.0.0.0/26 | 10.0.0.1 | PC1 (.1), PC2 (.2) |
| 20 | HR | 10.0.0.64/26 | 10.0.0.65 | PC3 (.65), PC4 (.66) |
| 30 | Sales | 10.0.0.128/26 | 10.0.0.129 | PC5 (.129), PC6 (.130) |

## ⚙️ What I Did

1. **Created VLANs** on the switch (VLAN 10, 20, 30) and named them Engineering, HR, and Sales.
2. **Assigned switch ports** to each VLAN as access ports:
   - F3/1, F4/1 → VLAN 10
   - F5/1, F6/1 → VLAN 20
   - F7/1, F8/1 → VLAN 30
3. **Connected the router to the switch** using a single trunk link (G1/1 on the router to a trunk port on the switch).
4. **Configured sub-interfaces** on the router (one per VLAN) with 802.1Q encapsulation, giving each VLAN its own gateway IP.
5. **Assigned static IP addresses** to all PCs within their respective VLAN subnets.
6. **Tested connectivity** using `ping` between devices in different VLANs to confirm inter-VLAN routing was working correctly.

## 🖥️ Sample Router Configuration

```bash
interface GigabitEthernet1/1
 no shutdown

interface GigabitEthernet1/1.10
 encapsulation dot1Q 10
 ip address 10.0.0.1 255.255.255.192

interface GigabitEthernet1/1.20
 encapsulation dot1Q 20
 ip address 10.0.0.65 255.255.255.192

interface GigabitEthernet1/1.30
 encapsulation dot1Q 30
 ip address 10.0.0.129 255.255.255.192
```

## 🖥️ Sample Switch Configuration

```bash
vlan 10
 name Engineering
vlan 20
 name HR
vlan 30
 name Sales

interface range FastEthernet3/1 - 4/1
 switchport mode access
 switchport access vlan 10

interface range FastEthernet5/1 - 6/1
 switchport mode access
 switchport access vlan 20

interface range FastEthernet7/1 - 8/1
 switchport mode access
 switchport access vlan 30

interface FastEthernet1/1
 switchport mode trunk
```

## ✅ Result
All PCs can successfully communicate:
- Within their own VLAN (same subnet).
- Across VLANs (via the router's sub-interfaces acting as gateways).

## 🛠️ Tools Used
- Cisco Packet Tracer

## 📸 Topology Diagram
See `VLAN-CONFIG-01.png` in this repository for the full network diagram.
