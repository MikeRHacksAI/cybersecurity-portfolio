# Incident‑004: Network Traffic Analysis — Beaconing Detection  
**Author:** Michael Roehr  
**Role:** SOC Analyst (Blue Team)  
**Tools:** Wireshark, Zeek, Suricata, Logseq  
**Date:** December 2025  

---

## 🎯 Objective  
Analyze suspicious outbound network traffic captured in a PCAP file. Determine whether the traffic represents command‑and‑control (C2) beaconing behavior.

---

## 📡 Traffic Summary  
- Repeated outbound HTTPS connections  
- Interval: every 60 seconds  
- Destination IP: 91.214.124.55  
- User-Agent: “Mozilla/5.0 (Windows NT 10.0)”  
- Packet sizes nearly identical across sessions  

---

## 🧪 Investigation Workflow  

### 1. Wireshark Review  
Key observations:  
- TLS handshake repeated at consistent intervals  
- No SNI value in the Client Hello  
- Packet sizes uniform, suggesting automated beaconing  
- No legitimate domain associated with the IP  

### 2. Zeek Analysis  
- JA3 fingerprint matched a known malware family  
- No HTTP headers or normal browsing patterns  
- TLS metadata consistent with C2 frameworks  

### 3. Suricata Alerts  
Suricata rule triggered:  
- “Possible C2 Beaconing Behavior”  
- Alert severity