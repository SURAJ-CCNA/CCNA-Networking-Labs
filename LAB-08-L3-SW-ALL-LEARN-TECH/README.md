L3 SWITCHING LAB: INTER-VLAN ROUTING WITH STATIC ROUTER

LAB OVERVIEW
================================================================================

This lab demonstrates Layer 3 switching with inter-VLAN routing using static routes. The setup uses a multilayer switch to route traffic between multiple VLANs without requiring a separate router.

Key Concepts Covered:
- VLAN configuration and management
- Trunk links between switches
- Static routing on a Layer 3 switch
- Inter-VLAN communication
- Network segmentation


NETWORK TOPOLOGY
================================================================================

Switch1 (VLAN 110) ──Trunk── Multilayer Switch (Layer 3 Switch)
Switch3 (VLAN 120) ──Trunk── + Router R3
Switch2 (VLAN 130) ──Trunk──


VLANS CONFIGURED
================================================================================

VLAN ID | Name           | Subnet              | Purpose
--------|----------------|---------------------|----------------------------
20      | Management     | 192.168.20.0/24     | Inter-switch link
110     | Department-A   | 192.168.110.0/24    | Laptop3, Laptop4
120     | Department-B   | 192.168.120.0/24    | Server, Laptop (Switch3)
130     | Department-C   | 192.168.130.0/24    | Laptop0, Laptop1 (Switch2)


LAYER 3 SWITCH CONFIGURATION
================================================================================

SVI Interfaces (Virtual IP Addresses):
- VLAN 20:   10.10.10.1/24
- VLAN 110:  192.168.110.1/24
- VLAN 120:  192.168.120.1/24
- VLAN 130:  192.168.130.1/24


STATIC ROUTES CONFIGURED
================================================================================

ip route 192.168.110.0 255.255.255.0 192.168.110.1
ip route 192.168.120.0 255.255.255.0 192.168.120.1
ip route 192.168.130.0 255.255.255.0 192.168.130.1
ip route 192.168.20.0 255.255.255.0 10.10.10.1


CONNECTED DEVICES
================================================================================

SWITCH 1 (Access Layer):
- Port fa0/24 → Laptop3 (VLAN 110) - 192.168.110.0/24
- Trunk to Multilayer Switch

SWITCH 3 (Access Layer):
- Port fa0/1 → Server (VLAN 120) - 192.168.120.0/24
- Port fa0/2 → Laptop (VLAN 120) - 192.168.120.0/24
- Trunk to Multilayer Switch

SWITCH 2 (Access Layer):
- Port fa0/3 → Laptop0 (VLAN 130) - 192.168.130.0/24
- Port fa0/4 → Laptop1 (VLAN 130) - 192.168.130.0/24
- Trunk to Multilayer Switch

EDGE DEVICES:
- PC1, PC2, PC3, PC4 connected to respective access ports
- Laptops distributed across VLANs for testing


TESTING & VALIDATION
================================================================================

Expected Connectivity:
✓ Devices in same VLAN: Direct communication via Layer 2
✓ Devices in different VLANs: Route through multilayer switch (Layer 3)
✓ All VLANs can reach management VLAN (20)

Test Commands:

Ping from Laptop3 (VLAN 110) to Server (VLAN 120):
ping 192.168.120.1

Ping from Laptop0 (VLAN 130) to Laptop3 (VLAN 110):
ping 192.168.110.1

Check routing table on multilayer switch:
show ip route

Verify VLAN configuration:
show vlan brief
show interfaces trunk


LEARNING OBJECTIVES
================================================================================

After completing this lab, you should understand:

1. VLAN Fundamentals - How to create and manage VLANs
2. Trunk Links - How switches communicate across multiple VLANs
3. Layer 3 Switching - Routing on a multilayer switch
4. Static Routing - Configuring static routes for inter-VLAN communication
5. Network Segmentation - Benefits of VLANs for security and performance


KEY CONFIGURATION STEPS
================================================================================

STEP 1: Create VLANs

vlan 110
name Department-A

vlan 120
name Department-B

vlan 130
name Department-C


STEP 2: Create SVI (Virtual Interfaces)

interface vlan 110
ip address 192.168.110.1 255.255.255.0
no shutdown

interface vlan 120
ip address 192.168.120.1 255.255.255.0
no shutdown

interface vlan 130
ip address 192.168.130.1 255.255.255.0
no shutdown


STEP 3: Configure Trunk Links

interface fa0/24
switchport mode trunk
switchport trunk allowed vlan all

interface g0/1
switchport mode trunk
switchport trunk allowed vlan all


STEP 4: Add Static Routes

ip route 192.168.110.0 255.255.255.0 192.168.110.1
ip route 192.168.120.0 255.255.255.0 192.168.120.1
ip route 192.168.130.0 255.255.255.0 192.168.130.1
ip route 192.168.20.0 255.255.255.0 10.10.10.1


HOW TO USE THIS LAB
================================================================================

1. Open in Cisco Packet Tracer - Load the .pkt file
2. Review the topology - Understand device placement
3. Configure switches - Follow the configuration steps above
4. Test connectivity - Use ping to verify inter-VLAN communication
5. Analyze traffic - Check "Simulation" mode to see packet flow


SECURITY NOTES
================================================================================

- VLANs provide logical segmentation (not security)
- For security, implement ACLs on the multilayer switch
- Restrict inter-VLAN traffic based on business requirements


TOPICS COVERED
================================================================================

✓ VLAN Configuration
✓ Trunk Encapsulation (802.1Q)
✓ Layer 3 Switching (Multilayer Switches)
✓ Static Routing
✓ SVI (Switched Virtual Interface)
✓ Inter-VLAN Routing


NEXT STEPS
================================================================================

Once this lab is mastered:
1. Add dynamic routing protocols (OSPF, EIGRP)
2. Implement ACLs for inter-VLAN filtering
3. Configure DHCP for automatic IP assignment
4. Add redundancy with STP (Spanning Tree Protocol)


RESOURCES
================================================================================

- Cisco VLAN Configuration Guide
- Layer 3 Switching Concepts
- CCNA Study Materials


INFORMATION
================================================================================

Created: July 2026
Simulator: Cisco Packet Tracer
Difficulty Level: Beginner-Intermediate
Estimated Time: 30-45 minutes

================================================================================
