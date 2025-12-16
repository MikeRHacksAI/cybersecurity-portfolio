# Incident‑000: Honeypot Email Infrastructure  
**Author:** Michael Roehr  
**Role:** SOC Analyst (Blue Team)  
**Tools:** Logseq, Python, SMTP/IMAP, Regex, Threat Intelligence Feeds  
**Date:** December 2025  

---

## 🎯 Objective  
Design and deploy a controlled honeypot email environment to safely collect, analyze, and classify malicious emails. The goal was to simulate a real corporate inbox, attract phishing attempts, and build a repeatable workflow for SOC analysis and reporting.

---

## 🏗️ Architecture Overview  

### Components  
- **Honeypot Mailbox:** A monitored inbox designed to attract phishing attempts  
- **Logseq Knowledge Graph:** Used for tagging, linking, and documenting incidents  
- **Python Automation:** Extracts headers, attachments, URLs, and indicators  
- **Threat Intel Sources:** VirusTotal, AbuseIPDB, URLScan, PhishTank  

### Data Flow  
1. Email arrives in honeypot inbox  
2. Python script extracts metadata + artifacts  
3. Indicators are enriched with threat intel  
4. Logseq auto‑links the incident to:
   - Sender profile  
   - Campaign type  
   - MITRE ATT&CK techniques  
   - Previous related incidents  

---

## 🧪 Sample Email Analysis Workflow  

### 1. **Header Analysis**  
- Extracted `Return‑Path`, `Received` chain, SPF/DKIM/DMARC  
- Identified mismatched domains and forged relay hops  
- Flagged anomalous sending infrastructure (e.g., VPS providers, open relays)

### 2. **Body & URL Analysis**  
- Parsed embedded URLs  
- Normalized obfuscated links (hex, base64, zero‑width characters)  
- Ran URLs through:
  - URLScan  
  - VirusTotal  
  - PhishTank  

### 3. **Attachment Analysis**  
- Extracted file metadata  
- Calculated hashes (MD5/SHA1/SHA256)  
- Submitted to sandbox for behavioral analysis  

### 4. **Threat Classification**  
Emails were categorized into:
- Credential phishing  
- Malware delivery  
- Business email compromise (BEC)  
- Spam / low‑risk noise  

---

## 🧩 Example Extracted Indicators  

| Indicator Type | Example | Notes |
|----------------|---------|-------|
| Sender Domain | `secure‑update‑team.com` | Newly registered, no DMARC |
| URL | `hxxps://login‑verify‑secure[.]com` | Credential harvesting |
| IP Address | `185.225.73.244` | Known phishing host |
| File Hash | `a9f0e61a137d86aa9db53465e0801612` | Malicious PDF |

---

## 🧠 MITRE ATT&CK Mapping  

| Technique | ID | How It Appeared |
|----------|----|------------------|
| Phishing | **T1566** | Email lure with fake login page |
| Command & Control | **T1071** | Malware beaconing via HTTPS |
| Credential Harvesting | **T1556** | Fake Microsoft 365 login portal |

---

## 📊 Metrics Collected  
- **Total emails analyzed:** 147  
- **Confirmed malicious:** 63  
- **Unique phishing campaigns:** 11  
- **New malicious domains discovered:** 22  
- **Average time to classify:** 3–5 minutes per email  

---

## 🧩 Lessons Learned  
- Threat actors frequently reuse infrastructure across campaigns  
- Newly registered domains (<30 days old) were the strongest phishing predictor  
- URL obfuscation techniques are increasing in complexity  
- Automating header + URL extraction reduced manual workload by ~70%  

---

## 🚀 Next Steps  
- Add automated YARA scanning for attachments  
- Expand honeypot to multiple “departments” (HR, Finance, IT)  
- Integrate with SIEM for real‑time alerting  
- Build dashboards for campaign clustering and trend analysis  

---

## 📁 Related Files  
- `/logseq-exports/Honeypot-Events.md`  
- `/diagrams/honeypot-architecture.png`  
- `/assets/sample-phishing-email.png`  
