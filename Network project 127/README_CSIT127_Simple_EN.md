# CSIT127 Packet Tracer Project — interconnected LANs (departments)

**Project file:** `CSIT127 project.pkt`  
**Author:** Timurmalik Djuraev (8562763)

## Overview (what this project is)
This Cisco Packet Tracer project demonstrates **multiple department LANs** connected together using **routers** (basic inter‑LAN routing).

From the topology screenshots:
- Department LANs: **Procurement**, **IT**, **HR**, **Staff**
- Each department has a **2960 switch** with wired end devices (PCs/laptops/printers)
- Some departments also have a **Wireless Access Point** for smartphones/tablets
- **Router0** connects the Procurement / IT / HR LANs
- **Router1** connects the Staff LAN
- **Router0 ↔ Router1** are linked to provide connectivity between all departments

> This is a straightforward design: **connected LANs + routing between them**. No advanced VPN/firewall/SIEM features are claimed unless you add them.

## Components (high level)
- **Routers:** 2 (Router0, Router1)
- **Switches:** 1 per department (multiple 2960 switches)
- **Wireless:** Access Points (for Wi‑Fi clients)
- **End devices:** PCs, laptops, printers, smartphones, tablets

## How to open the project
### Requirements
- Cisco Packet Tracer (recommended: v8.x)

### Steps
1. Open Cisco Packet Tracer
2. `File → Open`
3. Select **`CSIT127 project.pkt`**

## How to test (minimum checks)
1. **Ping inside the same department** (PC ↔ PC in the same LAN)
2. **Ping between departments** (e.g., IT ↔ HR, IT ↔ Staff, Procurement ↔ HR)
3. If printers are configured, verify reachability (ping the printer IP)

## Commands for screenshots (for your report)
### On routers
```
show ip interface brief
show ip route
show running-config
```

### On switches
If you did not configure VLANs, most ports will be in the default VLAN (VLAN 1).
```
show vlan brief
show interfaces status
show running-config
```

## Recommended repository structure
> Git/GitHub does not store empty folders — keep at least one file inside each folder (e.g., `README.md` or `.gitkeep`).

```
.
├─ CSIT127 project.pkt
├─ README.md
├─ screenshots/
│  ├─ topology.png
│  └─ tests/
├─ docs/
│  └─ report.docx (or report.pdf)
```

## What to include in the README / report (if required)
- Short description: “Department LANs are interconnected through routers”
- Topology screenshot/diagram
- IP addressing table (one subnet per department, if used)
- Proof of operation (pings + router routing table screenshots)

---
If you want, I can produce a **fully accurate README** with the **exact subnets, default gateways, and router interfaces**.
Just send:
- 1 screenshot of **IP Configuration** from one device in each department (IT/HR/Staff/Procurement), **or**
- Router0 + Router1 outputs: `show ip interface brief` and `show ip route`.
