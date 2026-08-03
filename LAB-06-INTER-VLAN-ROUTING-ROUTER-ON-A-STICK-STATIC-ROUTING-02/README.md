# InterVLAN Routing – Static Routing 02

## Overview

This lab demonstrates an enterprise-style network built using Cisco Packet Tracer.

The project combines Router-on-a-Stick, VLANs, Multiple Switches, Multiple Routers, and Static Routing to allow communication between multiple departments located on different networks.

---

# Technologies Used

- Cisco Packet Tracer
- Cisco ISR4331 Routers
- Cisco Catalyst 2950 Switches
- VLANs
- 802.1Q Trunking
- Router-on-a-Stick
- Static Routing
- IPv4 Addressing

---

# Network Topology

(Add topology.png here)

---

# VLAN Information

| VLAN | Department | Network | Gateway |
|------|------------|---------------|---------------|
|10|Sales|192.168.10.0/24|192.168.10.1|
|20|HR|192.168.20.0/24|192.168.20.1|
|30|IT|192.168.30.0/24|192.168.30.1|
|40|Finance|192.168.40.0/24|192.168.40.1|
|50|Canteen|192.168.50.0/24|192.168.50.1|
|60|ENTC Server|192.168.60.0/24|192.168.60.1|
|70|CSE|192.168.70.0/24|192.168.70.1|
|80|Mechanical Server|192.168.80.0/24|192.168.80.1|

---

# Device Configuration

---

## Router0 Configuration

### Interface

```
interface g0/0/0
no shutdown
```

### Router-on-a-Stick

```
interface g0/0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface g0/0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0

interface g0/0/0.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0

interface g0/0/0.50
encapsulation dot1Q 50
ip address 192.168.50.1 255.255.255.0

interface g0/0/0.60
encapsulation dot1Q 60
ip address 192.168.60.1 255.255.255.0
```

### Static Routes

```
ip route 192.168.70.0 255.255.255.0 10.10.10.2

ip route 192.168.80.0 255.255.255.0 10.10.10.2
```

---

## Router1 Configuration

### Interfaces

```
interface g0/0/0

ip address 10.10.10.2 255.255.255.252

no shutdown
```

```
interface g0/0/1

no shutdown
```

### VLAN80 Subinterface

```
interface g0/0/1.80

encapsulation dot1Q 80

ip address 192.168.80.1 255.255.255.0
```

### Physical Interface

```
interface g0/0/1

ip address 192.168.70.1 255.255.255.0
```

### Static Routes

```
ip route 192.168.10.0 255.255.255.0 10.10.10.1

ip route 192.168.20.0 255.255.255.0 10.10.10.1

ip route 192.168.30.0 255.255.255.0 10.10.10.1

ip route 192.168.40.0 255.255.255.0 10.10.10.1

ip route 192.168.50.0 255.255.255.0 10.10.10.1

ip route 192.168.60.0 255.255.255.0 10.10.10.1
```

---

## Switch0 Configuration

### Create VLANs

```
vlan 10
name SALES

vlan 20
name HR

vlan 30
name IT

vlan 40
name FINANCE

vlan 50
name CANTEEN

vlan 60
name ENTC
```

### Access Ports

```
interface fa0/1
switchport mode access
switchport access vlan 10

interface fa0/2
switchport mode access
switchport access vlan 20

interface fa0/3
switchport mode access
switchport access vlan 30

interface fa0/4
switchport mode access
switchport access vlan 40
```

### Router Trunk

```
interface g0/1

switchport mode trunk

switchport trunk allowed vlan 10,20,30,40,50,60
```

### Switch Trunk

```
interface g0/2

switchport mode trunk

switchport trunk allowed vlan 10,20,30,40,50,60
```

---

## Switch1 Configuration

### VLANs

```
vlan 10

vlan 50

vlan 60
```

### Access Ports

```
interface fa0/1

switchport mode access

switchport access vlan 10
```

```
interface fa0/2

switchport mode access

switchport access vlan 50
```

```
interface fa0/3

switchport mode access

switchport access vlan 60
```

### Trunk

```
interface g0/1

switchport mode trunk

switchport trunk allowed vlan 10,20,30,40,50,60
```

---

## Switch2 Configuration

### VLANs

```
vlan 70

vlan 80
```

### Access Ports

```
interface fa0/1

switchport mode access

switchport access vlan 70
```

```
interface fa0/2

switchport mode access

switchport access vlan 80
```

---

# Verification

Successful Tests

✅ VLAN10 ↔ VLAN60

✅ VLAN20 ↔ VLAN40

✅ VLAN30 ↔ VLAN50

✅ VLAN70 ↔ VLAN10

✅ VLAN80 ↔ VLAN60

✅ Router0 ↔ Router1

✅ Static Routing Verified

---

# Skills Demonstrated

- VLAN Configuration
- Inter-VLAN Routing
- Router-on-a-Stick
- Static Routing
- 802.1Q Trunking
- Multi-Switch Enterprise Design
- Multi-Router Communication
- Cisco IOS CLI
- Network Troubleshooting

---

# Author

**Suraj Bedekar**

B.Tech CSE (Cyber Security)

CCNA Student
