# 🛡️ Enterprise Network Security Assessment & Defense Planning

> A professional-grade network security assessment simulating the role of a Junior Cyber Security Analyst assigned to evaluate the security posture of a small-to-medium enterprise network.

---

## 📋 Project Overview

A company with **50–100 employees**, an internal LAN, internet-facing services, and Wi-Fi for employees and guests reported suspicious network behavior and requested a full security review. This project covers network architecture analysis, threat identification, vulnerability assessment, and defense strategy design.

**Role:** Junior Cyber Security Analyst  
**Organization:** Apex Solutions Pvt. Ltd. *(simulated)*  
**Assessment Type:** Internal Network Security Review  
**Classification:** Confidential — Pre-Remediation  
**Date:** March 2026

---

## 📁 Repository Contents

```
network-security-assessment/
│
├── network_security_assessment.docx   # Full 9-section audit report
├── network_diagram.svg                # Logical network topology diagram
├── risk_table.svg                     # Risk register (Threat → Impact → Mitigation)
└── README.md
```

---

## 📄 Deliverables

| File | Description |
|------|-------------|
| `network_security_assessment.docx` | 9-section professional report covering architecture, threats, vulnerabilities, defense strategy, and remediation roadmap |
| `network_diagram.svg` | Logical network topology with all zones annotated with live vulnerability callouts |
| `risk_table.svg` | 18-finding risk register with Threat → Likelihood → Impact → Risk Level → Mitigation |

---

## 🔍 Scope

| Component | Details |
|-----------|---------|
| Internal LAN | Wired corporate network — 10.10.0.0/22 |
| DMZ | Web server, email gateway, VPN endpoint |
| Server VLAN | Domain controller, file server, database |
| Management VLAN | Switch and router management interfaces |
| Employee Wi-Fi | SSID: CorpNet — 192.168.1.0/24 |
| Guest Wi-Fi | Isolated SSID — 192.168.2.0/24 |
| Endpoints | 50–100 workstations, laptops, mobile devices |

---

## 🚨 Key Findings Summary

| Severity | Count | Top Examples |
|----------|-------|-------------|
| 🔴 Critical | 3 | Internet-facing RDP (3389), SMBv1 enabled, Telnet on devices |
| 🟠 High | 6 | No MFA on VPN, 15 stale AD accounts, no SIEM, no EDR deployed |
| 🟡 Medium | 6 | WPA2-PSK Wi-Fi, no WIPS, TLS 1.0 active, dev server port 8080 exposed |
| 🟢 Low | 3 | Guest Wi-Fi client isolation, HTTP redirect missing, privileged account hygiene |

> **Overall Risk Rating: HIGH** — Immediate action required on all Critical findings before further network expansion or public service deployment.

---

## 🗺️ Network Zones Analyzed

```
[ INTERNET ]
     │
[ Edge Router ] — 203.0.113.1
     │
[ Perimeter Firewall ] ⚠ Internal logging disabled
     │
     ├──── [ DMZ ]  Web Server · Email Gateway · VPN ⚠ No MFA
     │
     ├──── [ Core Switch ]
     │          │
     │          ├── [ Corporate LAN ]   10.10.0.0/22  ⚠ SMBv1 Active
     │          ├── [ Server VLAN ]     10.10.4.0/24
     │          └── [ Management VLAN ] 10.10.5.0/24  ⚠ ACL Misconfiguration
     │
     └──── [ Wireless Controller ]
                │
                ├── [ Employee Wi-Fi ] 192.168.1.0/24  ⚠ WPA2-PSK, No WIPS
                └── [ Guest Wi-Fi ]   192.168.2.0/24  ⚠ Routing Leak
```

---

## 🛡️ Defense Recommendations

- **Firewall Rules** — Block RDP at perimeter, deny guest-to-internal routing, restrict DMZ-to-LAN paths
- **IDS/IPS Placement** — Deploy Suricata at internet edge, core switch SPAN port, and DMZ segment
- **Network Segmentation** — Full VLAN redesign with firewall-controlled inter-VLAN routing
- **Wi-Fi Hardening** — Migrate to WPA3-Enterprise with 802.1X / RADIUS authentication
- **Identity & Access** — Enforce MFA, disable stale accounts, implement PAM
- **Monitoring** — Deploy SIEM (Wazuh / Splunk), extend log retention to 90+ days

---

## 📅 Remediation Roadmap

| Priority | Action | Timeline |
|----------|--------|----------|
| P1 — Critical | Block RDP, disable SMBv1, disable Telnet, disable stale AD accounts | 24–48 hours |
| P2 — High | Deploy MFA on VPN, rotate device credentials, deploy EDR + SIEM | Week 1–2 |
| P3 — Medium | VLAN redesign, WPA3-Enterprise Wi-Fi, IDS/IPS deployment | Month 1–2 |
| P4 — Low | Guest Wi-Fi isolation, HTTPS enforcement, IR plan | Month 3–6 |

---

## 🧰 Tools & Frameworks Referenced

| Category | Details |
|----------|---------|
| Standards | NIST SP 800-115, CIS Controls v8, ISO/IEC 27001:2022 |
| IDS/IPS | Suricata, Snort 3 with Emerging Threats ruleset |
| SIEM | Wazuh, Splunk |
| EDR | CrowdStrike Falcon, Microsoft Defender ATP |
| Wi-Fi Security | WPA3-Enterprise, 802.1X, RADIUS |

---

## 🏆 Skills Gained

- ✅ Enterprise network architecture analysis
- ✅ Threat modeling and attack surface identification
- ✅ Risk scoring using Likelihood × Impact matrix
- ✅ Firewall rule design and IDS/IPS placement strategy
- ✅ Network segmentation and defense-in-depth planning
- ✅ Professional security report writing

---

## ⚠️ Disclaimer

> All scenarios, organizations, IP addresses, and findings in this project are entirely simulated for educational purposes. No real systems were accessed or tested.

---

<p align="center">
  <img src="https://img.shields.io/badge/Type-Network%20Security-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Framework-NIST%20SP%20800--115-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Standard-CIS%20Controls%20v8-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/Risk%20Rating-HIGH-red?style=flat-square"/>
</p>


