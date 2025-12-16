# Incident‑003: SIEM Alert — Brute Force Login Attempt  
**Author:** Michael Roehr  
**Role:** SOC Analyst (Blue Team)  
**Tools:** Splunk, Wazuh, Logseq, GeoIP, Python  
**Date:** December 2025  

---

## 🎯 Objective  
Investigate a SIEM alert indicating repeated failed login attempts against a Windows server. Determine whether the activity is malicious, identify the source, and recommend defensive actions.

---

## 🔔 Alert Summary  
- Alert Name: Excessive Authentication Failures  
- Source: Wazuh → Splunk  
- Target: WIN-SRV-01  
- User: administrator  
- Attempts: 87 failures in 3 minutes  

---

## 🧪 Investigation Workflow  

### 1. Log Review  
Splunk query used to isolate failed logins:

`index=windows EventCode=4625 user=administrator`

Findings:  
- All attempts originated from IP `103.145.12.77`  
- Username enumeration pattern observed  
- No successful authentication events  

### 2. GeoIP Lookup  
- Source IP geolocated to Vietnam  
- ASN associated with known brute-force botnet infrastructure  

### 3. Lateral Movement Check  
- No internal follow-up activity  
- No SMB, RDP, or WinRM connections from the target  
- No privilege escalation attempts detected  

###