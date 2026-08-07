# 🏢 Enterprise Multi-Switch Router-on-a-Stick Network Design

---

# 📌 Project Overview

This project demonstrates the design and implementation of a secure enterprise network using Cisco Packet Tracer.

The network is designed for a medium-sized organization with multiple departments separated into VLANs while allowing controlled communication through Router-on-a-Stick Inter-VLAN Routing.

The topology follows real enterprise networking practices including Layer-2 switching, Layer-3 routing, trunking, VLAN segmentation, and WAN connectivity between routers.

---

# 🎯 Objectives

- Design a scalable enterprise network
- Implement VLAN segmentation
- Configure Router-on-a-Stick
- Configure trunk links between switches
- Separate departments into individual broadcast domains
- Improve security using VLAN isolation
- Simulate real enterprise architecture
- Provide end-to-end connectivity between all departments

---

# 🏢 Network Topology

The network consists of:

- 2 Cisco ISR4331 Routers
- 4 Cisco 2960 Switches
- Multiple PCs
- Multiple Servers
- Inter-Switch Trunk Links
- Router-to-Router WAN Connection

---

# 🌐 Network Architecture

```
                    Router1
                       │
                 WAN Link
                       │
                    Router0
                       │
                  Core Switch
          ┌────────┼────────┐
          │        │        │
     Access     Access    Access
     Switch     Switch    Switch
          │        │        │
     VLAN Users VLAN Users VLAN Users
```

---

# 🖥 Devices Used

| Device | Quantity |
|----------|---------|
| Cisco ISR4331 Router | 2 |
| Cisco 2960 Switch | 4 |
| PCs | 7 |
| Servers | 2 |

---

# 📂 VLAN Design

| VLAN | Department | Network |
|-------|------------|----------------|
| VLAN 10 | HR | 192.168.10.0/24 |
| VLAN 20 | Security | 192.168.20.0/24 |
| VLAN 30 | IT | 192.168.30.0/24 |
| VLAN 40 | Finance | 192.168.40.0/24 |
| VLAN 50 | Administration | 192.168.50.0/24 |
| VLAN 60 | Server Farm | 192.168.60.0/24 |
| VLAN 70 | Management | 100.100.70.0/24 |

---

# 🌍 IP Addressing Scheme

| Network | Gateway |
|-----------|----------------|
| 192.168.10.0/24 | 192.168.10.1 |
| 192.168.20.0/24 | 192.168.20.1 |
| 192.168.30.0/24 | 192.168.30.1 |
| 192.168.40.0/24 | 192.168.40.1 |
| 192.168.50.0/24 | 192.168.50.1 |
| 192.168.60.0/24 | 192.168.60.1 |
| 100.100.70.0/24 | 100.100.70.1 |

---

# 🛠 Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- VLAN
- Router-on-a-Stick
- 802.1Q Trunking
- Static Routing
- WAN Routing
- Layer-2 Switching
- Layer-3 Routing

---

# ⚙ Features

✔ VLAN Segmentation

✔ Router-on-a-Stick

✔ Static Routing

✔ WAN Connectivity

✔ Inter-VLAN Communication

✔ Department Isolation

✔ Server Network

✔ Enterprise Network Design

✔ Multi-Switch Architecture

✔ Scalable Design

---

# 🔒 Security Features

- Separate VLAN for every department
- Broadcast domain isolation
- Trunk links carry only VLAN traffic
- Dedicated server VLAN
- Dedicated management VLAN
- Router-based Inter-VLAN routing
- Reduced broadcast traffic

---

# 📡 Traffic Flow

```
PC
 │
Access Switch
 │
802.1Q Trunk
 │
Core Switch
 │
Router-on-a-Stick
 │
Destination VLAN
 │
Target Device
```

---

# 📁 Project Structure

```
Enterprise-Network/
│
├── README.md
├── Enterprise-Network.pkt
├── Network-Topology.png
├── Configuration/
│     ├── Router0.txt
│     ├── Router1.txt
│     ├── Switch0.txt
│     ├── Switch1.txt
│     ├── Switch2.txt
│     └── Switch3.txt
│
├── Documentation/
│     ├── Project_Report.pdf
│     ├── Testing_Report.pdf
│     └── Screenshots/
│
└── LICENSE
```

---

# 🧪 Verification

Verify VLANs

```
show vlan brief
```

Verify Trunks

```
show interfaces trunk
```

Verify Interfaces

```
show ip interface brief
```

Verify Routes

```
show ip route
```

Test Connectivity

```
ping
```

---

# 🚀 Skills Demonstrated

- Enterprise Network Design
- Cisco CLI Configuration
- VLAN Configuration
- Inter-VLAN Routing
- Static Routing
- Trunk Configuration
- WAN Configuration
- Network Troubleshooting
- Layer-2 Switching
- Layer-3 Routing

---

# 🎓 Learning Outcomes

After completing this project, the following networking concepts were implemented and understood:

- VLAN Implementation
- Router-on-a-Stick
- Static Routing
- WAN Routing
- Switch Trunking
- Enterprise Network Planning
- IP Addressing
- Broadcast Domain Isolation
- Network Troubleshooting
- Cisco IOS CLI

---

# 📈 Future Improvements

- OSPF Routing
- DHCP Server
- NAT
- ACL
- SSH Remote Management
- Port Security
- EtherChannel
- HSRP
- STP Optimization
- Wireless LAN
- Firewall Integration
- IDS/IPS

---

# 👨‍💻 Author

**Sergio (Suraj Bedekar)**

B.Tech Computer Science Engineering

CCNA | Networking | Cyber Security

GitHub:
https://github.com/Sergio67byte

---

# ⭐ If you found this project useful, don't forget to star the repository.
