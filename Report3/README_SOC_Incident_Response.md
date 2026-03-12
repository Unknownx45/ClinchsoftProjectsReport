# 🚨 Cyber Security Incident Response & SOC Analysis Project

> A professional-grade incident response simulation acting as a SOC Tier-2 Analyst investigating and containing a real-world multi-vector cyber attack. Covers the full incident response lifecycle from detection through eradication, recovery, and lessons learned.

---

## 📋 Project Overview

NovaTech Systems Ltd. experienced a coordinated cyber attack involving brute-force credential theft, malware execution, C2 communication, lateral movement, and a data exfiltration attempt — all within a 90-minute window. This project documents the full SOC response lifecycle following **NIST SP 800-61 Rev 2** and maps attack activity to the **MITRE ATT&CK Framework**.

**Role:** SOC Tier-2 Analyst, Security Operations Center  
**Organization:** NovaTech Systems Ltd. *(simulated)*  
**Incident ID:** INC-2026-0312  
**Severity:** CRITICAL — P1  
**Date:** March 12, 2026  
**Report Status:** Final — Post-Incident Review

---

## 📁 Repository Contents

```
soc-incident-response/
│
├── incident_response_report.docx    # Full 8-section IR report
├── incident_timeline.svg            # Attack + response timeline (dark theme)
├── preventive_action_plan.svg       # 10-control post-incident action plan
└── README.md
```

---

## 📄 Deliverables

| File | Description |
|------|-------------|
| `incident_response_report.docx` | 8-section report covering identification, classification, containment, investigation, eradication, recovery, lessons learned, and closure |
| `incident_timeline.svg` | Dark-theme attack + SOC response timeline with MITRE ATT&CK mapping and key metrics |
| `preventive_action_plan.svg` | 10-control preventive action plan with priority tiers, deadlines, owners, and implementation roadmap |

---

## 🔴 Incident Summary

| Attribute | Details |
|-----------|---------|
| **Incident Type** | Multi-Vector: Brute Force + Malware (RAT) + Data Exfiltration Attempt |
| **Attack Entry Point** | VPN Gateway — credential brute force (no MFA) |
| **Malware** | AgentTesla RAT — delivered via phishing email attachment |
| **C2 Server** | 91.108.56.182 — RU (Selectel ASN) — HTTPS beacon every 30s |
| **Hosts Compromised** | WIN-WS-047, WIN-WS-061 |
| **Accounts Compromised** | j.mehta@novatech.in, admin-svc@novatech.in |
| **Data at Risk** | 240MB compressed archive — financial records directory |
| **Time to Contain** | 6 hours 42 minutes from detection |
| **Time to Recover** | 18 hours 28 minutes |
| **Confirmed Data Loss** | None (forensic investigation ongoing) |

---

## ⏱️ Attack & Response Timeline

```
~01:00  Attacker scans public IP range — identifies VPN on port 443
02:47   🔴 BRUTE FORCE BEGINS — 1,247 attempts in 8 min (TOR node 185.220.101.47)
02:47   ⚡ ALERT ALT-001 — SIEM detects auth spike; SOC paged
02:55   🔴 VPN BREACH — j.mehta credentials compromised; session established
03:12   🟠 MALWARE EXECUTES — invoice_Q1_2026.pdf.exe on WIN-WS-047
03:12   ⚡ ALERT ALT-002 — CrowdStrike EDR detects AgentTesla dropper
03:18   🟠 C2 BEACON — Encrypted HTTPS to 91.108.56.182:443 every 30s
03:22   🔵 SOC RESPONSE — WIN-WS-047 isolated; j.mehta account disabled
03:25   ✅ C2 SEVERED — Attacker loses shell; firewall blocks C2 IP
03:44   🟠 LATERAL MOVEMENT — admin-svc credentials harvested via LSASS dump
04:02   🔴 EXFILTRATION ATTEMPT — 240MB upload from WIN-WS-061
04:15   🟠 PERSISTENCE — Scheduled task created on both hosts
04:30   ✅ FULL CONTAINMENT — All attacker paths severed (T+6h42m)
09:29   🧹 ERADICATION — Both hosts fully reimaged
12:00   🔐 VPN RESTORED — MFA now enforced (Azure AD MFA + conditional access)
21:15   ✅ INCIDENT CLOSED — Environment verified clean (T+18h28m)
```

---

## 🗂️ MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name | Evidence |
|--------|-------------|----------------|---------|
| Reconnaissance | T1595 | Active Scanning | VPN port discovery |
| Initial Access | T1110.001 | Password Spraying | 1,247 auth attempts |
| Initial Access | T1133 | External Remote Services | VPN session from TOR |
| Execution | T1059.001 | PowerShell | Encoded C2 loader |
| Defense Evasion | T1055 | Process Injection | svchost.exe injection |
| C2 | T1071.001 | Web Protocols | HTTPS beacon |
| Lateral Movement | T1021.002 | SMB/Windows Admin Shares | Internal subnet scan |
| Credential Access | T1003.001 | LSASS Memory | Mimikatz-style dump |
| Exfiltration | T1048 | Exfiltration Over Alternative Protocol | 240MB HTTPS upload |
| Persistence | T1053.005 | Scheduled Task/Job | WindowsUpdateHelper task |

---

## 🛡️ Root Cause Analysis

| Root Cause | How It Enabled the Attack |
|-----------|--------------------------|
| **No MFA on VPN** *(primary)* | Brute-forced password granted full VPN access |
| Weak / reused password | j.mehta credential matched HIBP breach database |
| Outdated EDR signatures | 11 days behind; dropper bypassed detection for 2 minutes |
| No email attachment sandboxing | Malicious .exe reached inbox unchallenged |
| Excessive service account privileges | admin-svc had Domain Admin; lateral movement trivial |
| Flat LAN (no segmentation) | Single host could scan and reach entire internal /24 |
| DLP blind to HTTPS content | Exfiltration detected by volume only; extent unconfirmed |

---

## ✅ Post-Incident Preventive Controls

| # | Control | Priority | Deadline |
|---|---------|----------|----------|
| 01 | Enforce MFA on VPN & all remote access | 🔴 CRITICAL | 48 hours |
| 02 | Deploy email attachment sandboxing | 🔴 CRITICAL | 48 hours |
| 03 | EDR signature auto-update (every 4h) | 🔴 CRITICAL | 24 hours |
| 04 | Revoke excessive service account privileges | 🟠 HIGH | Week 1 |
| 05 | Network micro-segmentation (workstation VLANs) | 🟠 HIGH | Week 1–2 |
| 06 | Outbound HTTPS inspection / SSL DPI | 🟠 HIGH | Week 2 |
| 07 | UEBA — geographic & behavioral anomaly detection | 🟡 MEDIUM | Month 1 |
| 08 | Credential breach monitoring (HIBP integration) | 🟡 MEDIUM | Month 1 |
| 09 | Quarterly phishing simulations + awareness training | 🟢 ONGOING | Ongoing |
| 10 | IR plan review & annual tabletop exercises | 🟢 ONGOING | 6-monthly |

---

## 🧰 Tools & Frameworks Used

| Category | Tool / Standard |
|----------|----------------|
| IR Framework | NIST SP 800-61 Rev 2 |
| Attack Framework | MITRE ATT&CK v14 |
| SIEM | Wazuh + Splunk |
| EDR | CrowdStrike Falcon |
| Network IDS | Suricata (ET TROJAN ruleset) |
| Identity | Azure Active Directory + Conditional Access |
| DLP | Proxy-based volume anomaly detection |
| Compliance | ISO/IEC 27035 — Incident Management |

---

## 🏆 Skills Demonstrated

- ✅ SOC operations and alert triage
- ✅ Incident response lifecycle (NIST SP 800-61)
- ✅ Log and EDR telemetry analysis
- ✅ Attack chain reconstruction and root cause analysis
- ✅ MITRE ATT&CK framework mapping
- ✅ Containment and eradication planning
- ✅ Post-incident preventive controls design
- ✅ Professional incident report writing

---

## ⚠️ Disclaimer

> All scenarios, organizations, IP addresses, malware samples, and log entries in this project are entirely simulated for educational purposes. No real systems were accessed or tested.

---

<p align="center">
  <img src="https://img.shields.io/badge/Type-Incident%20Response-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/Framework-NIST%20SP%20800--61-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/ATT%26CK-10%20Techniques%20Mapped-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/Severity-CRITICAL%20P1-critical?style=flat-square"/>
  <img src="https://img.shields.io/badge/Outcome-Contained%20%26%20Resolved-green?style=flat-square"/>
</p>
