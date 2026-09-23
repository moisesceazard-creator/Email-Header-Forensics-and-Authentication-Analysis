# 🔬 Comparative Analysis: ESP Direct Delivery vs. Enterprise Cloud Signature Relay

A technical comparison between transactional bulk ESP routing (Coursera / SparkPost) and cloud-relayed corporate email (Ronin Research / M365 + Exclaimer Cloud) based on header forensics[cite: 16, 17].

---

## 📊 Architectural Comparison Matrix

| Feature | Case 01: Coursera (Bulk ESP) | Case 02: Ronin Research (Enterprise Relay) |
| :--- | :--- | :--- |
| **Primary Infrastructure** | SparkPost (`mta1vrest.sd.prd.sparkpost`)[cite: 16] | Microsoft 365 + Exclaimer Cloud[cite: 17] |
| **Delivery Mechanism** | Direct ESP-to-MX[cite: 16] | Loop-back Relay (M365 ➔ Exclaimer ➔ M365 ➔ Google)[cite: 17] |
| **Hop Count** | 3 Hops[cite: 16] | 8 Hops[cite: 17] |
| **Relay Latency** | 0 Seconds[cite: 16] | 7 Seconds[cite: 17] |
| **Intermediate SPF Status** | N/A (Direct Pass)[cite: 16] | `SoftFail` on `51.140.37.132` (Exclaimer IP)[cite: 17] |
| **Destination SPF Status** | **PASS** (`137.22.226.178`)[cite: 16] | **PASS** (`2a01:111:f403:c206::4`)[cite: 17] |
| **DKIM Selector** | `scph0823`[cite: 16] | `selector2`[cite: 17] |
| **DMARC Policy** | `p=REJECT`[cite: 16] | `p=NONE`[cite: 17] |
| **ARC Evaluation** | `i=1` (Single destination seal)[cite: 16] | `i=3` (Multi-stage preservation chain)[cite: 17] |

---

## 💡 Key Blue Team Insights

### 1. Handling Intermediate SPF Failures
In Case 02, Microsoft 365 logged `spf=softfail` when receiving traffic from `51.140.37.132`[cite: 17]. SOC Analysts must recognize that third-party relays (e.g., signature services, spam filters) often break standard SPF checks if their IPs are not included in the domain's SPF record or if `mailfrom` rewritten paths are altered[cite: 17].

### 2. The Critical Function of ARC
When messages pass through intermediate relays, ARC preserves original authentication details[cite: 17]. In Case 02, Google validated the ARC chain (`i=3 arc=pass`) to confirm that the message was legitimately signed and authenticated prior to intermediate handling[cite: 17].

### 3. DMARC Policy Maturity
* **Coursera (`p=REJECT`):** High security enforcement[cite: 16]. Prevents unauthorized actors from spoofing `@coursera.org`[cite: 16].
* **Ronin Research (`p=NONE`):** Monitoring mode[cite: 17]. Unauthenticated emails are delivered while administrators collect aggregate reports[cite: 17].
