# FUTURE_CS_1
<img width="1728" height="668" alt="image2" src="https://github.com/user-attachments/assets/ed61f70d-7a68-4055-9330-4ab8e06df068" />
<img width="943" height="1080" alt="image1" src="https://github.com/user-attachments/assets/ca98a853-4412-437f-82e3-fc5f70d92a2f" />
<img width="1536" height="474" alt="image4" src="https://github.com/user-attachments/assets/86aa0f8f-348c-455e-bbf5-be1fe72dfabd" />
<img width="1227" height="561" alt="image3" src="https://github.com/user-attachments/assets/a205819d-542e-4c68-8c67-7f329196b08f" />


# 🔐 Web Application Vulnerability Assessment Report
### Target: futureinterns.com | April 2026

![Security Grade](https://img.shields.io/badge/Security%20Grade-D-red)
![Findings](https://img.shields.io/badge/Total%20Findings-8-orange)
![High Risk](https://img.shields.io/badge/High%20Risk-1-critical)
![Medium Risk](https://img.shields.io/badge/Medium%20Risk-3-orange)
![Low Risk](https://img.shields.io/badge/Low%20Risk-4-yellow)
![Scope](https://img.shields.io/badge/Scope-Read--Only%20Passive-blue)
![Ethics](https://img.shields.io/badge/Ethics-OWASP%20Compliant-green)

---

## 📌 About This Project

This repository contains a **passive, read-only vulnerability assessment** conducted on `futureinterns.com` as part of a security consulting learning exercise. The assessment follows ethical guidelines — no exploitation, no brute force, no active attacks were performed.

The goal was to identify common web security misconfigurations that could expose the website or its users to risk, and present them in a professional, client-ready format.

---

## 🎯 Target Website

| Field | Details |
|---|---|
| **Target URL** | https://futureinterns.com |
| **IP Address** | 212.1.209.61 |
| **Web Server** | LiteSpeed |
| **Platform** | Hostinger (hPanel) |
| **Technology** | PHP 8.2.30 / WordPress |
| **Assessment Date** | April 12, 2026 |
| **Security Grade** | D (SecurityHeaders.com) |

---

## ⚠️ Scope of Testing

### ✅ Allowed (Performed)
- Public-facing HTTP/HTTPS pages only
- Passive header analysis using `curl`
- Automated header scanning via SecurityHeaders.com
- Network port enumeration using `nmap`
- Browser DevTools inspection (cookies, client-side)

### ❌ Not Allowed (Not Performed)
- Login bypass or authentication testing
- Exploitation of any vulnerability
- Brute force attacks
- SQL injection or XSS probing
- Denial-of-Service (DoS)
- Any activity that could harm the website or its users

> **Ethics Statement:** This assessment was conducted with strict adherence to ethical security principles. All testing was read-only and passive. No data was accessed, modified, or exfiltrated.

---

## 🛠️ Tools Used

| Tool | Purpose | Type |
|---|---|---|
| `curl` | Extract HTTP response headers | CLI |
| `nmap` | Port and service enumeration | CLI |
| SecurityHeaders.com | Automated security header grading | Web |
| Browser DevTools | Cookie flags and client-side inspection | Browser |
| Kali Linux | Testing environment | OS |

---

## 🔍 Findings Summary

| ID | Vulnerability | Location | Risk Level |
|---|---|---|---|
| F-01 | X-Powered-By Header Disclosure | HTTP Response Header | 🟡 Low |
| F-02 | Server & Platform Info Disclosure | HTTP Response Headers | 🟡 Low |
| F-03 | Missing Strict-Transport-Security (HSTS) | HTTP Response Header | 🔴 High |
| F-04 | Missing X-Frame-Options | HTTP Response Header | 🟠 Medium |
| F-05 | Missing X-Content-Type-Options | HTTP Response Header | 🟠 Medium |
| F-06 | Missing Referrer-Policy | HTTP Response Header | 🟡 Low |
| F-07 | Missing Permissions-Policy | HTTP Response Header | 🟡 Low |
| F-08 | Weak Content-Security-Policy | HTTP Response Header | 🟠 Medium |

---

## 🔴 Critical Finding — F-03: Missing HSTS Header

The most serious finding is the absence of the **HTTP Strict-Transport-Security (HSTS)** header.

Without HSTS, a network attacker (e.g., on a shared Wi-Fi network) can intercept traffic by forcing the browser to connect over unencrypted HTTP instead of HTTPS — even on a site that supports HTTPS.

**Fix:**
```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
```

---

## 🛡️ Top Remediation Steps

| Priority | Action | Estimated Effort |
|---|---|---|
| 1 — Urgent | Add Strict-Transport-Security header | < 30 min |
| 2 | Remove X-Powered-By, server, platform, panel headers | < 1 hour |
| 3 | Add X-Frame-Options: SAMEORIGIN | < 15 min |
| 4 | Add X-Content-Type-Options: nosniff | < 15 min |
| 5 | Strengthen Content-Security-Policy | 2–4 hours |
| 6 | Add Referrer-Policy header | < 15 min |
| 7 | Add Permissions-Policy header | < 15 min |

> All findings are header-based and can be fully remediated within a few hours by a developer or system administrator.

---

## 📁 Repository Structure

```
📦 vuln-assessment-futureinterns/
├── 📄 README.md                          ← This file
├── 📄 Vulnerability_Assessment_Report.pdf ← Full professional report
└── 📁 evidence/
    ├── 🖼️ 01_curl_header_output.png       ← curl -I response headers
    ├── 🖼️ 02_curl_full_headers.png        ← curl -s -D output
    ├── 🖼️ 03_securityheaders_grade.png    ← Grade D + missing headers
    ├── 🖼️ 04_securityheaders_raw.png      ← Raw headers detail
    └── 🖼️ 05_securityheaders_info.png     ← Additional info section
```

---

## 📊 Evidence

All evidence screenshots are located in the `/evidence` folder:

- **Screenshots 1–2:** `curl` terminal output showing disclosed headers (`x-powered-by`, `server`, `platform`, `panel`)
- **Screenshots 3–4:** SecurityHeaders.com scan results showing Grade D, missing headers list, and raw header values


[Vulnerability_Assessment_Report_futureinterns.docx](https://github.com/user-attachments/files/26925165/Vulnerability_Assessment_Report_futureinterns.docx)



---

## 📖 What I Learned

- How to perform a passive HTTP header analysis using `curl` on Kali Linux
- How to interpret security header scan results from SecurityHeaders.com
- How to classify vulnerabilities by risk level (Low / Medium / High)
- How to write a professional, client-ready vulnerability assessment report
- The real-world impact of common web security misconfigurations

---

## ⚖️ Disclaimer

This assessment was performed **for educational purposes only** as part of a security consulting learning exercise. All testing was strictly passive and read-only. No systems were harmed, modified, or exploited. The findings reflect the state of the target at the time of assessment (April 12, 2026).

---

*Prepared by: Security Audit Learner | Kali Linux | April 2026*
