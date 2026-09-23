# 📧 Enterprise Email Header Forensics & Authentication Analysis

A comprehensive Blue Team repository documenting real-world email header investigations, mail flow architectures, and authentication protocol breakdowns (SPF, DKIM, DMARC, ARC) following enterprise SOC triage standards.

---

## 👤 Analyst Profile

**Moises Ceazar Del Mundo, CC**  
*Security Operations Center (SOC) Analyst / Threat Hunter*

---

## 🎯 Repository Purpose

Email remains the primary attack vector for enterprise breaches. This repository demonstrates practical skills in:
- Deconstructing complex SMTP relay paths and hop latencies.
- Validating email authentication mechanisms (**SPF**, **DKIM**, **DMARC**, **ARC**).
- Differentiating legitimate third-party Email Service Providers (ESPs) and Cloud Signature Relays from spoofing/phishing vectors.
- Performing triage using industry tools like **MXToolbox**, **Google Admin Toolbox**, and EDR/SEG logs.

---

## 📊 Investigated Cases Index

| Case ID | Subject / Source Domain | Mail Infrastructure | Key Forensics Topic | DMARC Policy | Status |
| :---: | :--- | :--- | :--- | :---: | :---: |
| **CASE-001** | `coursera.org` | SparkPost (Bulk ESP) | Direct ESP Delivery & Strict DMARC Enforcement | `p=REJECT` | 🟢 Analyzed |
| **CASE-002** | `roninresearch.com` | M365 + Exclaimer Cloud | Multi-hop Relay & ARC Authentication Preservation | `p=NONE` | 🟢 Analyzed |

---

## 🔬 Comparative Architectural Analysis

### Case 001 vs. Case 002: Key Authentication & Flow Differences
