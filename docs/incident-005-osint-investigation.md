# Incident‑005: OSINT Investigation — Malicious Domain Infrastructure  
**Author:** Michael Roehr  
**Role:** SOC Analyst (Blue Team)  
**Tools:** WHOIS, Passive DNS, VirusTotal, Shodan, Logseq  
**Date:** December 2025  

---

## 🎯 Objective  
Investigate a suspicious domain discovered during phishing analysis. Map the threat actor’s infrastructure and identify related malicious assets.

---

## 🌐 Domain Summary  
- Domain: `secure-login-verification[.]com`  
- Registrar: Namecheap  
- Domain Age: 5 days  
- Category: Phishing / Credential Harvesting  

---

## 🧪 Investigation Workflow  

### 1. WHOIS Lookup  
Findings:  
- WHOIS privacy enabled  
- Registered using cryptocurrency  
- Registrar associated with multiple malicious domains  

### 2. Passive DNS  
Related domains discovered:  
- `secure-login-check[.]net`  
- `microsoft-auth-verify[.]com`  
- `office365-security-alert[.]org`  

These domains share:  
- Similar naming patterns  
- Same hosting provider  
- Same IP block  

### 3. Shodan Scan  
Shodan revealed:  
- Open ports: 80, 443  
- Self‑signed SSL certificate  
- Hosting provider linked to phishing campaigns  
- No legitimate services or business presence  

### 4. VirusTotal  
- Multiple engines flagged the domain as phishing  
- Passive DNS showed repeated short‑lived domains on same IP  

### 5. Classification  
**Phishing Infrastructure Cluster (High Confidence)**

---

## 🧩 Extracted Indicators  

| Type | Value | Notes |
|------|--------|-------|
| Domain | secure-login-verification[.]com | Malicious |
| IP | 185.225.73.244 | Shared phishing host |
| SSL Cert | Self-signed | Suspicious, non‑legitimate |
| Related Domains | microsoft-auth-verify[.]com | Same infrastructure |

---

## 🧠 MITRE ATT&CK Mapping  

| Technique | ID | Description |
|-----------|----|-------------|
| Reconnaissance | T1595 | Active scanning and discovery |
| Resource Development | T1583 | Domain registration for malicious use |
| Phishing | T1566 | Credential harvesting infrastructure |

---

## 🚀 Next Steps  
- Add all related domains and IPs to blocklists  
- Monitor for new registrations with similar naming patterns  
- Automate OSINT enrichment for future phishing investigations  
- Share indicators with threat intelligence feeds  
