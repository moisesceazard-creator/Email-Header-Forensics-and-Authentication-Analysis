# 🔍 CASE-001: Coursera Mail Flow Triage (SparkPost ESP)

**Analyst:** Moises Ceazar Del Mundo, CC  
**Target Recipient:** `moisesceazard@gmail.com`[cite: 16]  
**Verdict:** 🟢 Legitimate Transactional Email (Passes SPF, DKIM, and DMARC)[cite: 16]  

---

## 📊 Header Summary & Metadata

| Field | Value |
| :--- | :--- |
| **Header From** | `coursera.org`[cite: 16] |
| **Envelope From (Return-Path)** | `msprvs1=20724T78Eo4Xd=bounces-266693-993@m.learn.coursera.org`[cite: 16] |
| **Sending IP** | `137.22.226.178` (`vy8stkzx.m.learn.coursera.org`)[cite: 16] |
| **Originating MTA** | `i-05ead51dbbc3cbc22.mta1vrest.sd.prd.sparkpost`[cite: 16] |
| **Recipient MX** | `mx.google.com`[cite: 16] |
| **Total Relay Delay** | 0 seconds[cite: 16] |

---

## 🔄 Hop Path & Relay Trace

1. **Hop 1 (Origin):**  
   * **From:** `10.90.14.248`[cite: 16]  
   * **By:** `i-05ead51dbbc3cbc22.mta1vrest.sd.prd.sparkpost`[cite: 16]  
   * **Protocol:** REST[cite: 16]  
   * **Timestamp:** `9/21/2026 3:55:31 PM`[cite: 16]  

2. **Hop 2 (Egress to Destination):**  
   * **From:** `vy8stkzx.m.learn.coursera.org` (`137.22.226.178`)[cite: 16]  
   * **By:** `mx.google.com`[cite: 16]  
   * **Protocol:** ESMTPS[cite: 16]  
   * **Delay:** 0 seconds[cite: 16]  

---

## 🛡️ Authentication Results

* **SPF Evaluation:**  
  * **Result:** **PASS**[cite: 16]  
  * **Details:** `google.com: domain of msprvs1=20724t78eo4xd=bounces-266693-993@m.learn.coursera.org designates 137.22.226.178 as permitted sender`[cite: 16].  

* **DKIM Evaluation:**  
  * **Result:** **PASS**[cite: 16]  
  * **Domain:** `m.learn.coursera.org`[cite: 16]  
  * **Selector:** `scph0823`[cite: 16]  

* **DMARC Evaluation:**  
  * **Result:** **PASS**[cite: 16]  
  * **Header From:** `coursera.org`[cite: 16]  
  * **Policy (`p`):** `REJECT`[cite: 16]  
  * **Subdomain Policy (`sp`):** `REJECT`[cite: 16]  
  * **Disposition:** `NONE`[cite: 16]  

* **ARC Seal:**  
  * `i=1` sealed by `google.com` (`s=arc-20260327`, `cv=none`)[cite: 16].

---

## 🎯 Key Forensic Findings

* **Infrastructure Pattern:** The sender utilizes SparkPost as an external Email Service Provider (ESP) for transactional communications[cite: 16].
* **Strict Enforcement:** The parent domain `coursera.org` enforces `p=REJECT`[cite: 16]. Unauthenticated emails pretending to originate from this domain will be rejected by compliance-enabled gateways[cite: 16].
