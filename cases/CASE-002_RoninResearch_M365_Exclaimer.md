# 🔍 CASE-002: Ronin Research Mail Flow Triage (M365 + Exclaimer Relay)

**Analyst:** Moises Ceazar Del Mundo, CC  
**Target Recipient:** `moisesceazardelmundo@gmail.com`[cite: 17]  
**Verdict:** 🟢 Legitimate Enterprise Mail (Multi-hop Cloud Relay with Valid ARC)[cite: 17]  

---

## 📊 Header Summary & Metadata

| Field | Value |
| :--- | :--- |
| **Header From** | `roninresearch.com`[cite: 17] |
| **Envelope From (Return-Path)** | `<Jasmin.Decena@roninresearch.com>`[cite: 17] |
| **Outbound IPv6 (To Google)** | `2a01:111:f403:c206::4` (`CWXP265CU010.outbound.protection.outlook.com`)[cite: 17] |
| **Intermediate Relay IP** | `51.140.37.132` (`uk1.smtp.exclaimer.net`)[cite: 17] |
| **Total Hop Count** | 8 Hops[cite: 17] |
| **Total Relay Delay** | 7 seconds[cite: 17] |

---

## 🔄 Hop Path & Relay Trace

1. **Hop 1 (Origin M365 Mailbox):** `LO0P265MB9082.GBRP265.PROD.OUTLOOK.COM` via MAPI[cite: 17].
2. **Hop 2 (Internal M365 Move):** `LO8P265MB7579.GBRP265.PROD.OUTLOOK.COM` via TLS1[cite: 17].
3. **Hop 3 (Egress to Exclaimer):** `LO2P265CU024.outbound.protection.outlook.com` (`40.93.67.26`) to `uk1.smtp.exclaimer.net` (`51.140.37.132`)[cite: 17].
4. **Hop 4 (Exclaimer Ingestion):** `uk1.smtp.exclaimer.net` to `AM3PEPF00009B9D.mail.protection.outlook.com`[cite: 17].
5. **Hop 5 (Internal M365 Processing):** `AM3PEPF00009B9D.eurprd04.prod.outlook.com` to `AM0P309CA0011.outlook.office365.com`[cite: 17].
6. **Hop 6 (Internal M365 Processing):** `AM0P309CA0011.EURP309.PROD.OUTLOOK.COM` to `LO7P265MB7714.GBRP265.PROD.OUTLOOK.COM`[cite: 17].
7. **Hop 7 (Final Egress to Destination):** `CWXP265CU010.outbound.protection.outlook.com` (`2a01:111:f403:c206::4`) to `mx.google.com`[cite: 17].
8. **Hop 8 (Google Ingest):** Google local delivery (`2002:a05:6521:2246:b0:341:d95:7af5`)[cite: 17].

---

## 🛡️ Authentication Results & Relay Anomalies

* **Intermediate M365 Evaluation (Exclaimer Return):**  
  * `X-MS-Exchange-Authentication-Results: spf=softfail (sender IP is 51.140.37.132) smtp.mailfrom=roninresearch.com`[cite: 17].  
  * **Reason:** When Exclaimer (`51.140.37.132`) returned the email to M365, M365 evaluated SPF against the Exclaimer server IP, resulting in an intermediate `SoftFail`[cite: 17].

* **Final Google MX Evaluation:**  
  * **SPF:** **PASS** (`domain of jasmin.decena@roninresearch.com designates 2a01:111:f403:c206::4 as permitted sender`)[cite: 17].  
  * **DKIM:** **PASS** (`header.i=@roninresearch.com`, selector `selector2`)[cite: 17].  
  * **DMARC:** **PASS** (`p=NONE`, `sp=NONE`, `dis=NONE`)[cite: 17].  
  * **ARC Evaluation:** **PASS** (`i=3`, `arc=pass (i=2 dkim=pass dkdomain=roninresearch.com dmarc=pass fromdomain=roninresearch.com)`)[cite: 17].

---

## 🎯 Key Forensic Findings

* **Signature Management Integration:** The domain routes outbound messages through Exclaimer Cloud (`uk1.smtp.exclaimer.net`) to inject standardized corporate email signatures (`X-ExclaimerHostedSignatures-MessageProcessed: true`)[cite: 17].
* **Role of ARC:** Microsoft applied ARC seals (`i=1` and `i=2`) before sending the message out to Google[cite: 17]. Google used ARC (`i=3`) to verify that authentication was successful prior to the Exclaimer relay, preventing false positives caused by the intermediate SPF `SoftFail`[cite: 17].
