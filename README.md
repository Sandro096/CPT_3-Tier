# 🌐 Cisco Packet Tracer — 3-Tier Hierarchical Enterprise Network

A fully functional enterprise network simulation built in **Cisco Packet Tracer**, following the Cisco 3-tier hierarchical model. The project covers a complete network from WAN connectivity down to end-user devices, including routing, VLANs, DHCP, NAT, DNS, FTP, and inter-VLAN security policies.

---

## 📋 Project Overview

This lab simulates a realistic corporate network divided into three departments:

| Department | VLAN | Subnet |
|---|---|---|
| IT | VLAN 10 | 192.168.10.0/24 |
| IT Failover (DHCP) | VLAN 11 | 192.168.11.0/24 |
| HR | VLAN 20 | 192.168.20.0/24 |
| Administration | VLAN 30 | 192.168.30.0/24 |

---

## 🏗️ Network Architecture

```
                        [ WAN / Cloud-PT ]
                       /                  \
                     C1                    C2          ← Core Layer
                    /  \                  /  \
                  R1     \-------R2-------/    R3      ← Distribution Layer
                  |              |             |
                  S1             S2            S3      ← Access Layer L3 (3560)
                 / \             /\            /\
               A1  A2          A3  A4        A5  A6    ← Access Layer L2 (2960)
```

### Layers

- **Core** — C1, C2 (Router 2911): WAN connectivity via serial links, NAT overload (PAT), OSPF
- **Distribution** — R1, R2, R3 (Router 2911): Inter-layer routing with OSPF
- **Access L3** — S1, S2, S3 (Switch 3560): VLAN gateways via SVI, DHCP relay, OSPF
- **Access L2** — A1-A6 (Switch 2960): VLAN segmentation for end devices

---

## ✅ Features Implemented

- **OSPF** (area 0) across all routers and L3 switches
- **NAT overload (PAT)** on C1 and C2 toward WAN
- **DHCP** with primary and secondary server (failover simulation)
- **DHCP relay** (`ip helper-address`) across VLANs
- **DNS** server with internal A records
- **FTP/NAS** server with role-based user access
- **Web server** (HTTP/HTTPS) hosting the company intranet
- **Inter-VLAN ACLs** enforcing department-level security policies
- **WAN redundancy** via dual core routers

---

## 🔒 Security Policy (ACLs)

| Source | Destination | Access |
|---|---|---|
| IT (VLAN 10) | All VLANs | ✅ Full access |
| HR (VLAN 20) | DNS, DHCP, Web Server | ✅ Allowed |
| HR (VLAN 20) | FTP/NAS, Admin VLAN | ❌ Blocked |
| Admin (VLAN 30) | DNS, DHCP, Web Server | ✅ Allowed |
| Admin (VLAN 30) | FTP/NAS, HR VLAN | ❌ Blocked |

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `network_report.docx` | Full lab report with all configurations, IP tables, and test results |
| `network.pkt` | Original Cisco Packet Tracer project file |
| `README.md` | This file |

---

## 🧪 Test Results

All end-to-end tests passed:

- ✅ DHCP assignment across all VLANs
- ✅ Inter-VLAN routing (IT ↔ HR ↔ Admin)
- ✅ DNS resolution (`nslookup intranet.azienda.local`)
- ✅ Web server reachable via browser and domain name
- ✅ FTP access restricted to IT only
- ✅ NAT translations verified (`show ip nat translations`)
- ✅ ACLs blocking unauthorized inter-VLAN traffic

---

## 🛠️ Tools Used

- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)

---

## 📄 Documentation

For full device configurations, IP addressing tables, DHCP pools, ACL rules, and test results, refer to the attached **[network_report.docx](./network_report.docx)**.

---

## 🗂️ Packet Tracer Project File

The original **`network.pkt`** file is included in this repository so you can open, explore, and reproduce the entire lab directly in Cisco Packet Tracer — all devices, connections, and configurations are already in place.
