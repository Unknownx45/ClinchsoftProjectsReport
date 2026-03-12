# 🔐 Cybersecurity Analyst Portfolio

> Three end-to-end security projects simulating real-world roles: Network Security Analyst, Web Application Security Analyst, and SOC Analyst. Each project includes professional reports, visual deliverables, and GitHub-ready documentation.

<p align="left">
  <img src="https://img.shields.io/badge/Projects-3-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Framework-OWASP%20%7C%20NIST%20%7C%20MITRE%20ATT%26CK-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/Role-Junior%20SOC%20%2F%20Security%20Analyst-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Reports-Professional%20Grade-blueviolet?style=flat-square"/>
</p>

---

## 📁 Repository Structure

```
cybersecurity-portfolio/
├── 01-network-security-assessment/
│   ├── network_security_assessment.docx
│   ├── network_diagram.svg
│   ├── risk_table.svg
│   └── README.md
├── 02-web-application-security-audit/
│   ├── web_security_audit.docx
│   ├── owasp_mapping.svg
│   ├── security_checklist.svg
│   └── README.md
├── 03-soc-incident-response/
│   ├── incident_response_report.docx
│   ├── incident_timeline.svg
│   ├── preventive_action_plan.svg
│   └── README.md
└── README.md  ← You are here
```

---

## 📌 Project 1 — Network Security Assessment

**Scenario:** Apex Solutions Pvt. Ltd. (50–100 employees) reports suspicious network activity and requests a full infrastructure security review.

**Key Findings:**

| Severity | Count | Top Issues |
|----------|-------|-----------|
| 🔴 Critical | 3 | RDP exposed to internet, SMBv1 enabled, Telnet active |
| 🟠 High | 6 | No MFA on VPN, stale AD accounts, no SIEM, no EDR |
| 🟡 Medium | 6 | WPA2-PSK Wi-Fi, no WIPS, TLS 1.0, dev server exposed |

**Deliverables:** Audit report · Network topology diagram · Risk register (18 findings)  
**Frameworks:** NIST SP 800-115 · CIS Controls v8 · ISO/IEC 27001

---

## 📌 Project 2 — Web Application Security Audit

**Scenario:** PortalX (React / Node.js / PostgreSQL) requests a pre-launch security review before going public.

**Key Findings:**

| Severity | Count | Top Issues |
|----------|-------|-----------|
| 🔴 Critical | 2 | SQL Injection (CVSS 9.8), Stored XSS (CVSS 9.3) |
| 🟠 High | 4 | Broken auth, unrestricted file upload, IDOR, MD5 passwords |
| 🟡 Medium | 6 | Missing headers, no CSRF, no rate limiting, vulnerable deps |

> ❌ **Verdict: Not ready for public launch** — critical findings block go-live.

**Deliverables:** Audit report with code-level fixes · OWASP mapping table · 47-item hardening checklist  
**Frameworks:** OWASP Top 10 (2021) · CVSS v3.1 · NIST SP 800-115

---

## 📌 Project 3 — SOC Incident Response

**Scenario:** NovaTech Systems Ltd. is hit by a multi-vector attack — brute force → malware → C2 → lateral movement → data exfiltration attempt (Incident ID: INC-2026-0312).

**Incident at a Glance:**

| Metric | Value |
|--------|-------|
| Attack Vector | VPN brute force → phishing email |
| Malware | AgentTesla RAT (C2: 91.108.56.182, RU) |
| Hosts Affected | WIN-WS-047, WIN-WS-061 |
| Time to Contain | 6 hours 42 minutes |
| Time to Recover | 18 hours 28 minutes |
| Data Loss | None confirmed |

**Deliverables:** Full IR report · Attack timeline (dark theme) · 10-control preventive action plan  
**Frameworks:** NIST SP 800-61 Rev 2 · MITRE ATT&CK (10 techniques mapped) · ISO/IEC 27035

---

## 🏆 Skills Demonstrated

| Area | Skills |
|------|--------|
| **Network Security** | Architecture analysis, threat modeling, firewall design, segmentation |
| **Web App Security** | OWASP Top 10, code-level vulnerability analysis, secure coding |
| **Incident Response** | SOC workflows, log analysis, MITRE ATT&CK mapping, IR lifecycle |
| **Documentation** | Professional reports, risk registers, timelines, action plans |

---

## ⚠️ Disclaimer

> All scenarios, organizations, IP addresses, and findings are entirely simulated for educational purposes. No real systems were accessed or tested.
