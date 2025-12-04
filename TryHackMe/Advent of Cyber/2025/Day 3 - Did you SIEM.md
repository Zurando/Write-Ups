# TryHackMe Write-Up — Splunk for Log Analysis  
**Author:** Zurando  
**Room:** https://tryhackme.com/room/splunkforloganalysis-aoc2025-x8fj2k4rqp  
**Concept:** Splunk Log Searching & Threat Investigation  

---

## Overview  
My goal with this room is to sharpen my ability to analyse logs using Splunk, identify malicious patterns, and follow an attacker’s activity across different log sources.  
This write-up covers my approach to navigating Splunk, filtering event data, analysing malicious traffic, and extracting key insights from web and firewall logs.

---

# Method of Solve

## Initial Setup in Splunk  
1. Click the **Search and Reporting** app (green button, top-left).  
2. In the **New search** bar, enter:  
```
index=main
```
3. Set the time range to **All time** (left of the magnifying glass).  
4. Under **INTERESTING FIELDS**, select `user_agent`.  
5. From the list, select:  
**Havij/1.17 (Automated SQL Injection)**  

---

# Q1 — What is the attacker IP found attacking and compromising the web server?  
All returned logs show attacks originating from:  
**198.51.100.55**

---

# Q2 — Which day was the peak traffic in the logs? (Format: YYYY-MM-DD)  
1. Run:  
```
index=main sourcetype=web_traffic
| timechart span=1d count
| sort by count
```
2. Look at the bar graph at the top of the Splunk interface.  
3. The highest event volume occurred on:  
**2025-10-12**

---

# Q3 — What is the count of Havij user_agent events found in the logs?  
1. Under **INTERESTING FIELDS**, open **user_agent**.  
2. The entry:  
**Havij/1.17 (Automated SQL Injection)**  
shows a **Count** of:  
**993**

---

# Q4 — How many path traversal attempts to access sensitive files were observed?  

1. Identify attacker IP: `198.51.100.55`  
2. Filter for web traffic from that IP:  
```
index=main sourcetype=web_traffic client_ip="198.51.100.55" 
```
3. Filter for potential path traversal activity:  
```
index=main sourcetype=web_traffic client_ip="198.51.100.55" AND path="*..*" 
| stats count by path
```
4. Splunk reports **658** matching events.

**Answer:** **658**

---

# Q5 — How many bytes were transferred to the C2 server IP from the compromised web server?  

### Known Information
- Compromised web server IP: `10.10.1.5`  
- Malicious/C2 IP: `198.51.100.55`

### Search Query  
Filter for firewall logs where the compromised server contacted the C2:
```
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="198.51.100.55"
```
Filter for allowed traffic:
```
AND action="ALLOWED"
```
Sum all bytes transferred:
```
| stats sum(bytes_transferred) by src_ip
```
### Full Query
```
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="198.51.100.55" AND action="ALLOWED" 
| stats sum(bytes_transferred) by src_ip
```

### Result  
**126167 bytes**

---

## Summary  
This room helped reinforce Splunk fundamentals, including:  
- Running targeted search queries  
- Investigating malicious user-agents  
- Tracking attacker activity across IPs  
- Identifying peak traffic windows  
- Aggregating data from firewall logs  

A strong foundation for deeper SIEM and log analysis work.
