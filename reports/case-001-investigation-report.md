# SOC Phishing Email Investigation Report
**Case ID:** CASE-001
**Classification:** RESTRICTED — For Educational/Portfolio Use Only

## 1. Incident Overview

| Field | Details |
|---|---|
| **Incident ID** | CASE-001-PHISHING-2026 |
| **Date/Time of Alert** | Tue, 07 Apr 2026 04:29:26 +0000 |
| **Analyst Name** | Satya Upendra Samana |
| **Reporter / Department** | Self-reported — Personal Email Inbox |
| **Status** | Malicious — Confirmed |
| **Incident Description** | Analyst received a recruitment email from hr@zorvyn.io claiming to offer a Cybersecurity Analyst Intern role at Zorvyn FinTech. Email contained a unique-token screening link, a tracking pixel, and originated from a domain with zero DNS infrastructure. Investigation confirmed Recruitment Phishing targeting job-seeking freshers on LinkedIn. |

## 2. Email Metadata

| Field | Details |
|---|---|
| **Sender Display Name** | HR - Zorvyn |
| **Sender Email Address** | hr@zorvyn.io |
| **Recipient** | 22MH1A0313@acoe.edu.in |
| **Subject Line** | Screening Assessment for Cybersecurity Analyst Intern Role - Zorvyn |
| **Date / Timestamp** | Tue, 07 Apr 2026 04:29:26 +0000 |

## 3. Header Analysis

| Field | Details |
|---|---|
| **Return-Path** | Not present — abnormal for legitimate corporate email |
| **Reply-To** | hr@zorvyn.io |
| **Source IP** | Masked via Exchange routing |
| **Originating Server** | Microsoft ExchangeLabs |

### Authentication Results

| Protocol | Result | Notes |
|---|---|---|
| **SPF** | Not verifiable | zorvyn.io has no DNS records |
| **DKIM** | Not verifiable | No MX or TXT records exist |
| **DMARC** | Not verifiable | Domain entirely offline |

## 4. Threat Indicators (IOCs)

### Suspicious URLs

**URL 1 — Screening Link**
| Field | Details |
|---|---|
| **URL** | https://screening.zorvyn.io/e/3/cIAmrgD4E77_YQop84VmeFn8bOMrIZ5t |
| **Type** | Credential harvesting portal |
| **Token** | cIAmrgD4E77_YQop84VmeFn8bOMrIZ5t — victim-specific |
| **DNS** | NXDOMAIN — taken down |
| **Risk** | CRITICAL |

**URL 2 — Tracking Pixel**
| Field | Details |
|---|---|
| **URL** | https://hrapi.zorvyn.io/api/v1/analytics/track/OAEPi5y9yiz92iNQzb_EMg.png |
| **Type** | 1x1 invisible tracking pixel |
| **Purpose** | Captures victim IP, location, device info on email open |
| **DNS** | NXDOMAIN |
| **Risk** | HIGH |

**URL 3 — Azure Logo**
| Field | Details |
|---|---|
| **URL** | https://companyasset.blob.core.windows.net/assets/zorvynfulllogodark.png |
| **Type** | Image asset on Microsoft Azure |
| **Purpose** | Appear legitimate, evade email filters |
| **Risk** | SUSPICIOUS |

**URL 4 — Main Domain**
| Field | Details |
|---|---|
| **URL** | https://www.zorvyn.io/ |
| **DNS** | NXDOMAIN — no website exists |
| **Risk** | HIGH |

### Attachments
No attachments detected.

## 5. Email Body & Content Analysis

| Field | Details |
|---|---|
| **Tone** | Moderate urgency — time-sensitive job opportunity |
| **Social Engineering** | Exploits job-seeking behavior targeting freshers on LinkedIn |
| **Formatting** | Professional — deliberate effort to appear legitimate |
| **Branding** | Logo hosted on Azure to appear credible |
| **Request Type** | Data harvesting via screening assessment portal |
| **Target Profile** | Fresh graduates in IT/Cybersecurity applying on LinkedIn |

## 6. Investigation Findings

### DNS Investigation

| Query | Result |
|---|---|
| zorvyn.io A | NXDOMAIN |
| zorvyn.io MX | NXDOMAIN |
| www.zorvyn.io A | NXDOMAIN |
| screening.zorvyn.io A | NXDOMAIN |
| WHOIS Registrant | Privacy Protected |
| Domain Age | ~1 year |

### OSINT Summary

| Source | Finding |
|---|---|
| LinkedIn | 103k followers, verified, 44 members — likely purchased followers |
| AmbitionBox | 1 star, 7 reviews — reviewers likely victims |
| Web | No verifiable company presence |

### MITRE ATT&CK Mapping

| Technique | ID |
|---|---|
| Phishing for Information | T1598 |
| Establish Accounts | T1585 |
| Social Media Attack Vector | T1585.001 |
| Gather Victim Identity Info | T1589 |

### Verdict
MALICIOUS — Recruitment Phishing / Job Scam
Confidence: HIGH

The email originated from hr@zorvyn.io — a domain with zero DNS infrastructure. It contained a victim-specific screening link and a tracking pixel for passive profiling. No verifiable company presence exists outside LinkedIn. AmbitionBox reviews confirm multiple victims. Entire zorvyn.io infrastructure taken down post-campaign — consistent with hit-and-run phishing targeting job-seeking freshers.

## 7. Remediation & Action Taken

| Field | Details |
|---|---|
| **Analyst Status** | Email flagged — screening link not clicked |
| **Email Disposition** | Archived for evidence — marked as phishing |
| **Blocked Indicators** | zorvyn.io and all subdomains flagged |
| **Escalation** | Report fake LinkedIn page to LinkedIn Trust & Safety |

## 8. Tools Used

| Tool | Purpose |
|---|---|
| REMnux Linux | Isolated analysis environment |
| cat + grep | Email header extraction |
| dig | DNS investigation |
| whois | Domain registration lookup |
| grep -Eo | URL extraction from raw email |
| LinkedIn / AmbitionBox | OSINT on company legitimacy |

---
Report prepared by: Satya Upendra Samana
Analysis Environment: REMnux on VirtualBox
Date of Analysis: June 2026
