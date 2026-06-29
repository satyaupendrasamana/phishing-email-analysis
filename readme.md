# Phishing Email Analysis — Case 001

## Overview
Real-world phishing investigation conducted inside REMnux VM.
Analyzed a recruitment phishing email targeting job-seeking freshers on LinkedIn.

## Case Summary
- **Case ID:** CASE-001-PHISHING-2026
- **Verdict:** Malicious — Recruitment Phishing / Job Scam
- **Target:** Cybersecurity fresher actively applying for jobs
- **Threat Actor:** Fake fintech company operating as Zorvyn (zorvyn.io)

## Tools Used
- REMnux Linux (isolated analysis environment)
- dig (DNS investigation)
- whois (domain registration lookup)
- grep (header and URL extraction)
- LinkedIn / AmbitionBox (OSINT)

## Investigation Steps
1. Extracted email headers to identify sender metadata
2. Extracted all URLs embedded in the email body
3. Performed DNS lookup on sender domain (zorvyn.io)
4. Conducted WHOIS analysis on domain registration
5. OSINT investigation via LinkedIn and AmbitionBox
6. Documented all IOCs and mapped to MITRE ATT&CK

## Key Findings
- zorvyn.io has zero DNS infrastructure (NXDOMAIN on all records)
- Email contained a victim-specific tracking pixel
- Screening link contained unique token for victim tracking
- Domain WHOIS registrant is privacy protected
- AmbitionBox shows 1 star rating — multiple victims confirmed
- LinkedIn page has 103k followers — likely purchased for credibility

## MITRE ATT&CK Mapping
| Technique | ID |
|---|---|
| Phishing for Information | T1598 |
| Establish Accounts | T1585 |
| Social Media Attack Vector | T1585.001 |
| Gather Victim Identity Info | T1589 |

## Folder Structure
Case-001-Phishing-Investigation/

├── samples/        — raw .eml and .msg files

├── artifacts/      — extracted headers, URLs, DNS results

├── screenshots/    — terminal evidence screenshots

├── reports/        — full SOC investigation report

└── readme.md       — this file


## Analyst
Satya Upendra Samana
SOC Analyst Fresher | Google Cybersecurity Certified
