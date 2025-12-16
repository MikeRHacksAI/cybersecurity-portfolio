# Incident‑001: Phishing Investigation — Fake Microsoft 365 Login  
**Author:** Michael Roehr  
**Role:** SOC Analyst (Blue Team)  
**Tools:** Logseq, Python, URLScan, VirusTotal, WHOIS, IMAP  
**Date:** December 2025  

---

## 🎯 Objective  
Investigate a suspicious email claiming to be a Microsoft 365 password reset request. Determine whether the email is malicious, extract indicators, analyze the phishing infrastructure, and document findings for future detection tuning.

---

## 📨 Email Summary  
- **Subject:** “Your Microsoft 365 Password Will Expire Today”  
- **Sender:** `security-update@office365-support.com`  
- **Recipient:** Honeypot mailbox  
- **Attachment:** None  
- **Body:** Urgent request to “verify your account”  

---

## 🧪 Investigation Workflow  

### 1. **Header Analysis**  
- SPF: **Fail**  
- DKIM: **None**  
- DMARC: **Fail**  
- Return‑Path domain mismatched sender domain  
- Received chain showed relay through a VPS provider in Eastern Europe  

### 2. **URL Analysis**  
Extracted phishing URL:

