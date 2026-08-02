# 🚀 CCNA Lab 05- Inter-VLAN Routing (Router-on-a-Stick)


# 📌 Project Overview

This lab demonstrates **Inter-VLAN Routing using Router-on-a-Stick (ROAS)**.

A single router physical interface is connected to the switch using an **802.1Q Trunk Link**. The router creates multiple **subinterfaces**, allowing devices in different VLANs to communicate with each other.

This is one of the most important practical labs in the Cisco CCNA 200-301 syllabus.

---

# 🎯 Objective

- Create multiple VLANs
- Configure Access Ports
- Configure a Trunk Port
- Configure Router Subinterfaces
- Enable communication between different VLANs
- Verify connectivity using Ping

---

# 🏢 Network Topology

```
                    Router
                 (ISR4331 / 2911)
                     G0/0
                      |
               802.1Q Trunk
                      |
                Cisco 2960 Switch
      ---------------------------------
      |         |         |           |
     PC0       PC1       PC2        PC3
   VLAN10    VLAN20    VLAN30     VLAN40
```

---

# 📡 VLAN Information

| VLAN | Department | Network | Default Gateway |
|------|------------|----------------|----------------|
|10|Sales|192.168.10.0/24|192.168.10.1|
|20|HR|192.168.20.0/24|192.168.20.1|
|30|IT|192.168.30.0/24|192.168.30.1|
|40|Finance|192.168.40.0/24|192.168.40.1|

---

# 💻 PC Configuration

## PC0

```
IP Address : 192.168.10.10
Subnet Mask: 255.255.255.0
Gateway    : 192.168.10.1
```

## PC1

```
IP Address : 192.168.20.10
Subnet Mask: 255.255.255.0
Gateway    : 192.168.20.1
```

## PC2

```
IP Address : 192.168.30.10
Subnet Mask: 255.255.255.0
Gateway    : 192.168.30.1
```

## PC3

```
IP Address : 192.168.40.10
Subnet Mask: 255.255.255.0
Gateway    : 192.168.40.1
```

---

# ⚙️ Switch Configuration

## Create VLANs

```bash
enable
configure terminal

vlan 10
name SALES

vlan 20
name HR

vlan 30
name IT

vlan 40
name FINANCE
```

---

## Configure Access Ports

### VLAN 10

```bash
interface fa0/1
switchport mode access
switchport access vlan 10
```

### VLAN 20

```bash
interface fa0/2
switchport mode access
switchport access vlan 20
```

### VLAN 30

```bash
interface fa0/3
switchport mode access
switchport access vlan 30
```

### VLAN 40

```bash
interface fa0/4
switchport mode access
switchport access vlan 40
```

---

## Configure Trunk Port

```bash
interface g0/1
switchport mode trunk
```

---

# ⚙️ Router Configuration

## Enable Physical Interface

```bash
enable

configure terminal

interface g0/0

no shutdown
```

---

## Configure Subinterfaces

### VLAN 10

```bash
interface g0/0.10

encapsulation dot1Q 10

ip address 192.168.10.1 255.255.255.0
```

---

### VLAN 20

```bash
interface g0/0.20

encapsulation dot1Q 20

ip address 192.168.20.1 255.255.255.0
```

---

### VLAN 30

```bash
interface g0/0.30

encapsulation dot1Q 30

ip address 192.168.30.1 255.255.255.0
```

---

### VLAN 40

```bash
interface g0/0.40

encapsulation dot1Q 40

ip address 192.168.40.1 255.255.255.0
```

---

## Save Configuration

```bash
end

copy running-config startup-config
```

---

# 🔍 Verification Commands

## Switch

```bash
show vlan brief

show interfaces trunk

show running-config
```

---

## Router

```bash
show ip interface brief

show running-config

show ip route
```

---

# 🧪 Testing

From any PC

```
ping 192.168.20.10

ping 192.168.30.10

ping 192.168.40.10
```

Successful replies confirm that **Inter-VLAN Routing is working correctly.**

---

# 🧠 Concepts Learned

✅ VLAN

✅ Access Port

✅ Trunk Port

✅ IEEE 802.1Q

✅ Router-on-a-Stick

✅ Router Subinterfaces

✅ Inter-VLAN Routing

✅ Default Gateway

✅ Ping Testing

---

# 📚 Key Learning

Without a router, devices in different VLANs cannot communicate because each VLAN is a separate broadcast domain.

Router-on-a-Stick solves this problem by using one physical router interface with multiple logical subinterfaces. Each subinterface acts as the default gateway for one VLAN, allowing the router to route traffic between VLANs over a single trunk link.

---

# 🎓 CCNA Topics Covered

- VLAN Configuration
- Trunk Configuration
- IEEE 802.1Q Encapsulation
- Router Subinterfaces
- Inter-VLAN Routing
- Network Verification
- Basic Troubleshooting

---

# 🛠️ Software Used

- Cisco Packet Tracer
- Cisco ISR4331 / Cisco 2911 Router
- Cisco 2960 Switch

---

# 👨‍💻 Author

**Suraj Bedekar**

B.Tech CSE (Cyber Security Honors)

Cisco CCNA 200-301 Student

GitHub:
https://github.com/Sergio67byte

---

⭐ If you found this lab useful, feel free to star the repository.
