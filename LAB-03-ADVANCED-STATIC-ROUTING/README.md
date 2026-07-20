# Lab 3: Static Routing with Redundant Paths (5 Routers + 3 LANs)

## 🎯 Objective
Configure static routing across 5 routers connecting 3 LANs, with multiple redundant paths between routers for fault tolerance.

## 📐 Topology
- **LAN-01:** 192.168.10.0/24 → Router-01
- **LAN-02:** 192.168.20.0/24 → Router-04
- **LAN-03:** 192.168.30.0/24 → Router-03

**Redundancy:** Router-03 and Router-04 have a direct link (10.10.50.0/30) in addition to routing through Router2 — creates 2 possible paths between them.

## 🖥️ Equipment Used
- 5x Cisco 2911 Routers (Router-01, Router2, Router-03, Router-04, Router-05)
- 3x Cisco 2960-24TT Switches
- Multiple PCs, Laptops, and Servers across 3 LANs

## ✅ Test Results

| Test | Result |
|------|--------|
| LAN-01 to LAN-02 | ✅ SUCCESS |
| LAN-01 to LAN-03 | ✅ SUCCESS |
| LAN-02 to LAN-03 | ✅ SUCCESS |
| Redundant path (R03-R04 direct link) | ✅ Working |

## 💡 Key Learnings

- Static routing scaled to 3 LANs (up from 2 in previous lab)
- Redundant router links provide backup paths if one link fails
- Mesh-style topology planning for fault tolerance
- More routes required per router as LAN count increases
- Real-world relevance: this mirrors how companies connect multiple office branches

## 🐛 Notes

- All routers required routes to reach every other LAN (not just direct neighbors)
- Redundant link between Router-03 and Router-04 tested by verifying an alternate path exists

---

**Status:** ✅ Complete | **Tool:** Cisco Packet Tracer | **Date:** [JULY-2027]
