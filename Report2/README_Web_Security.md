# 🌐 Web Application Security Review & Vulnerability Analysis

> A professional-grade web application security audit simulating the role of a Web Security Analyst performing a pre-launch review of a customer-facing application, mapped against the OWASP Top 10 (2021).

---

## 📋 Project Overview

A development team requested a security review of their web application — *PortalX* — before public launch. The application features a login system, user dashboard, and multiple interactive forms handling sensitive user data. This project covers input validation, authentication, session management, access control, file upload security, and server configuration.

**Role:** Web Security Analyst  
**Application:** PortalX — Customer Web Portal *(simulated)*  
**Tech Stack:** React 18 / Node.js + Express / PostgreSQL  
**Assessment Type:** Pre-Launch Security Review  
**Framework:** OWASP Top 10 (2021)  
**Date:** March 2026

---

## 📁 Repository Contents

```
web-application-security-audit/
│
├── web_security_audit.docx     # Full 6-section audit report with code-level findings
├── owasp_mapping.svg           # 14 findings mapped to OWASP Top 10 categories
├── security_checklist.svg      # 47-item pre-launch security hardening checklist
└── README.md
```

---

## 📄 Deliverables

| File | Description |
|------|-------------|
| `web_security_audit.docx` | 6-section report with vulnerable code snippets, attack demos, and secure code fixes for each finding |
| `owasp_mapping.svg` | All 14 findings mapped to OWASP category, severity badge, CVSS score, business impact, and attack vector |
| `security_checklist.svg` | 47-item hardening checklist across 8 categories — tagged Mandatory / High / Recommended / Best Practice |

---

## 🚨 Vulnerability Findings

| ID | Vulnerability | Severity | OWASP (2021) | CVSS |
|----|--------------|----------|--------------|------|
| VF-01 | SQL Injection — login endpoint | 🔴 Critical | A03 — Injection | 9.8 |
| VF-02 | Stored XSS — profile bio/display name | 🔴 Critical | A03 — Injection | 9.3 |
| VF-03 | Broken Authentication (weak JWT, no lockout) | 🟠 High | A07 — Auth Failures | 8.1 |
| VF-04 | Unrestricted File Upload (RCE risk) | 🟠 High | A04 — Insecure Design | 7.5 |
| VF-05 | Broken Access Control / IDOR | 🟠 High | A01 — Broken Access Control | 7.5 |
| VF-06 | Missing Security Headers (CSP, HSTS, etc.) | 🟡 Medium | A05 — Misconfiguration | 6.1 |
| VF-07 | Sensitive Data Exposure (MD5, PII in logs) | 🟡 Medium | A02 — Crypto Failures | 6.5 |
| VF-08 | No CSRF Protection | 🟡 Medium | A01 — Broken Access Control | 5.4 |
| VF-09 | No Rate Limiting on auth endpoints | 🟡 Medium | A07 — Auth Failures | 5.3 |
| VF-10 | Vulnerable Dependencies (axios, lodash, multer) | 🟡 Medium | A06 — Vuln. Components | 5.9 |
| VF-11 | Weak Password Hashing — MD5 no salt | 🟠 High | A02 — Crypto Failures | 7.2 |
| VF-12 | HTTPS Not Enforced on all routes | 🟡 Medium | A02 — Crypto Failures | 5.4 |
| VF-13 | Error / Stack Trace Information Disclosure | 🟢 Low | A05 — Misconfiguration | 3.7 |
| VF-14 | Debug Mode Enabled in Production | 🟢 Low | A05 — Misconfiguration | 3.1 |

> **Audit Verdict: ❌ NOT READY FOR PUBLIC LAUNCH** — All Critical and High findings must be resolved and re-tested before go-live sign-off.

---

## 🗂️ OWASP Top 10 Coverage

```
A01 — Broken Access Control      ██░░░░░░░░  2 findings  (VF-05, VF-08)
A02 — Cryptographic Failures     ███░░░░░░░  3 findings  (VF-07, VF-11, VF-12)
A03 — Injection                  ██░░░░░░░░  2 findings  (VF-01, VF-02)
A04 — Insecure Design            █░░░░░░░░░  1 finding   (VF-04)
A05 — Security Misconfiguration  ███░░░░░░░  3 findings  (VF-06, VF-13, VF-14)
A06 — Vulnerable Components      █░░░░░░░░░  1 finding   (VF-10)
A07 — Auth Failures              ██░░░░░░░░  2 findings  (VF-03, VF-09)
```

---

## 🔎 Sample Finding — SQL Injection (VF-01)

**Vulnerable Code:**
```javascript
// ❌ VULNERABLE — Direct string concatenation
const query = "SELECT * FROM users WHERE email = '" + email + "' AND password = '" + password + "'";
db.query(query);
```

**Attack Payload:**
```
email: ' OR '1'='1' --
password: (anything)
→ Bypasses authentication entirely; returns all users
```

**Secure Fix:**
```javascript
// ✅ SECURE — Parameterized query
const query = 'SELECT * FROM users WHERE email = $1 AND password = $2';
db.query(query, [email, hashedPassword]);
```

---

## ✅ Security Checklist Highlights

**Mandatory (block launch):**
- [ ] Replace all raw SQL with parameterized queries
- [ ] Remove `dangerouslySetInnerHTML` — sanitize with DOMPurify
- [ ] Replace MD5 with bcrypt (cost ≥ 12) or Argon2id
- [ ] Move JWT secret to environment variable; validate `exp` claim
- [ ] Add server-side ownership check on all resource endpoints
- [ ] Validate file MIME type via magic bytes server-side
- [ ] Patch npm CVEs: axios, lodash, multer

**High priority (week 1):**
- [ ] Implement account lockout after 5 failed attempts
- [ ] Set cookie flags: `HttpOnly; Secure; SameSite=Strict`
- [ ] Invalidate sessions on logout and password change
- [ ] Replace sequential IDs with UUIDs
- [ ] Add Content-Security-Policy and HSTS headers
- [ ] Re-encode all file uploads through Sharp

---

## 🧰 Tools & Frameworks Referenced

| Category | Tools |
|----------|-------|
| Assessment Framework | OWASP Top 10 (2021), CVSS v3.1 |
| Static Analysis (SAST) | Semgrep, ESLint-security, SonarQube |
| Dynamic Testing (DAST) | OWASP ZAP, Burp Suite Community |
| Dependency Scanning | npm audit, Snyk, Dependabot |
| Secrets Detection | GitLeaks, TruffleHog |
| WAF | AWS WAF, Cloudflare |
| Libraries | DOMPurify, validator.js, bcrypt, Argon2 |

---

## 📅 Remediation Schedule

| Priority | Finding(s) | Deadline | Owner |
|----------|-----------|----------|-------|
| P1 — Critical | VF-01 SQL Injection, VF-02 Stored XSS | 48 hours | Backend Dev |
| P2 — High | VF-03 Auth, VF-11 MD5 Passwords | Week 1 | Auth Team |
| P2 — High | VF-04 File Upload, VF-05 IDOR | Week 1 | Backend Dev |
| P3 — Medium | VF-06 Headers, VF-08 CSRF, VF-09 Rate Limiting | Week 2–3 | DevOps |
| P3 — Medium | VF-07 Data Exposure, VF-10 Dependencies, VF-12 HTTPS | Week 2–3 | Full Stack |
| P4 — Low | VF-13 Error Disclosure, VF-14 Debug Mode | Week 3–4 | DevOps |

---

## 🏆 Skills Gained

- ✅ Web application architecture and data flow analysis
- ✅ Code-level vulnerability identification (SQLi, XSS, IDOR)
- ✅ OWASP Top 10 (2021) risk mapping
- ✅ CVSS v3.1 severity scoring
- ✅ Secure coding practices with before/after code examples
- ✅ Security testing methodology (SAST, DAST, dependency scanning)
- ✅ Professional web security audit report writing

---

## ⚠️ Disclaimer

> All scenarios, application names, code samples, and findings in this project are entirely simulated for educational purposes. No real systems, applications, or user data were accessed or tested.

---

<p align="center">
  <img src="https://img.shields.io/badge/Type-Web%20App%20Security-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Framework-OWASP%20Top%2010%202021-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/Scoring-CVSS%20v3.1-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/Verdict-Not%20Ready%20for%20Launch-critical?style=flat-square"/>
</p>
