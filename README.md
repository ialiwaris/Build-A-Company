
# About Project: Enterprise Network Infrastructure

| Status   | Visibility         | Version |
|----------|-------------------|---------|
| ✅ Deployed | 🔒 Internal Use Only (No Personal Data Included) | v1.0 |

---

## Project Summary
This document outlines the structure and segmentation of a secure enterprise network, designed with multiple VLAN-backed zones, a central firewall, and strict access policies. The architecture enforces the Zero Trust principle, allowing communication only where explicitly defined.

---

## Network Zones & VLAN Mapping

| Zone Name         | VLAN ID | Subnet           | Purpose                                 |
|-------------------|---------|------------------|-----------------------------------------|
| Production        | v10     | 10.204.10.0/24   | Core business apps and internal services|
| Monitoring        | v11     | 10.204.11.0/24   | Tools like Grafana, log analyzers|
| Storage           | v12     | 10.204.12.0/24   | Backup systems, file storage            |
| Management        | v13     | 10.204.13.0/24   | Admin access: SSH, RDP, AD, syslog      |
| Servers (General) | v14     | 10.204.14.0/24   | Internal service nodes (e.g. DNS, DHCP) |
| DMZ               | v15     | 10.204.15.0/24   | Public-facing apps & reverse proxies    |

---

## Firewall Policy Overview

| Source Zone | Destination Zone | Allowed Services                                 |
|-------------|------------------|-------------------------------------------------|
| Management  | All Zones        | SSH, RDP, WinRM (admin ports only)              |
| Monitoring  | All Zones        |  ICMP, Syslog                              |
| DMZ         | Internet         | HTTP/HTTPS only                                 |
| Servers     | Specific Zones   | Based on role (e.g., DNS, DHCP)                 |
| Storage     | None             | No outbound access (inbound from Prod only)     |
| Inter-Zone  | All              | Denied by default (Least Privilege)             |

---

## Security Controls

- 🔒 Zone-based segmentation using VLANs
- 🔥 Stateful firewall between all zones
- 📡 Monitoring enabled across all interfaces
- 🧱 Default-Deny firewall model
- 🧑‍💻 Management Zone isolated from user/production traffic
- 🗂️ Storage Zone has no internet or DMZ access

---

## Network Flow Diagram

```
[Internet]
    ↓
[Edge Router]
    ↓
[Firewall]
    ↓
──────────── VLAN Trunk ─────────────
| v10 | v11 | v12 | v13 | v14 | v15 |
```
All zones are trunked over VLAN-aware switches and terminated at a firewall for zone isolation and inter-VLAN routing.

---

✅ Designed for security, visibility, and scalability.

