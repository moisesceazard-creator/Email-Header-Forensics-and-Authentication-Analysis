# 📧 Enterprise Email Header Forensics & Authentication Repository

Documentation of enterprise email header triage, mail flow path analysis, and authentication mechanism evaluation (**SPF**, **DKIM**, **DMARC**, and **ARC**) following SOC Standard Operating Procedures.

---

## 👤 Analyst Profile

**Moises Ceazar Del Mundo, CC**  
*Security Operations Center (SOC) Analyst*

---

## 🛠️ Key Technical Competencies Demonstrated

- **Mail Routing Forensics:** Extracting bottom-to-top SMTP hops, IP origins, and relay latency.
- **Protocol Verification:** Evaluating cryptographic signatures (**DKIM**) and domain authorization (**SPF**).
- **Policy Enforcement Analysis:** Assessing DMARC disposition policies (`p=none`, `p=reject`) and domain alignment.
- **Authenticated Received Chain (ARC):** Analyzing multi-seal ARC chains (`i=1`, `i=2`, `i=3`) to trace authentication state across intermediate cloud relays.

---

## 📊 Investigated Cases Index

| Case ID | Source Domain | Infrastructure | Key Technical Topic | DMARC Policy | Status |
| :---: | :--- | :--- | :--- | :---: | :---: |
| **CASE-001** | `coursera.org` | SparkPost (Bulk ESP) | Direct ESP Delivery & Strict Policy Enforcement | `p=REJECT`[cite: 16] | 🟢 Complete |
| **CASE-002** | `roninresearch.com` | M365 + Exclaimer Relay | Cloud Signature Routing & ARC Authentication Preservation | `p=NONE`[cite: 17] | 🟢 Complete |

---

## 📑 Repository Structure

* `cases/CASE-001_Coursera_SparkPost_ESP.md`: Triage of direct bulk mailing infrastructure[cite: 16].
* `cases/CASE-002_RoninResearch_M365_Exclaimer.md`: Triage of enterprise M365 routing via third-party signature relay[cite: 17].
* `comparative_analysis/ESP_vs_Enterprise_Relay.md`: Architectural breakdown comparing ESP direct delivery with enterprise signature relays[cite: 16, 17].
