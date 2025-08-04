# 🛡️ Spring4Shell Malware Attack - Incident Postmortem

## 📅 Incident Overview

A critical malware attack exploiting the **Spring4Shell** vulnerability led to a service outage on the **NBN infrastructure** managed by Telstra. The attack caused remote code execution on exposed systems and service downtime.

---

## ⚠️ Incident Details

- **Start Time:** 2022-03-20T03:16:34Z  
- **End Time:** 2022-03-20T05:16:34Z  
- **Status:** Resolved  
- **Severity:** 1 (Critical)  
- **Detection Time:** 2022-03-20T03:16:34Z  
- **Root Cause Fix Time:** 2022-03-20T02:16:34Z (Pre-deployed)

---

## 👥 Participants

- Telstra Security Operations  
- NBN Services Team  
- Telstra Networks Team  

---

## 🧨 Impact Summary

- Remote code execution on `nbn.external.network`  
- HTTP POST request payload targeting `/tomcatwar.jsp`  
- Downtime and degraded performance for NBN services  
- High volume of customer complaints  

---

## 🕵️‍♂️ Root Cause

The attacker used a known **Spring4Shell PoC** to send HTTP POST requests with malicious query strings targeting a vulnerable endpoint. The payload enabled RCE (Remote Code Execution) via:

- Exploit: `Spring4Shell`  
- Path: `/tomcatwar.jsp`  
- Method: `POST`  
- Protocol: `HTTP/1.1`  

---

## 🔍 Detection & Response Timeline

1. **Detection:** Firewall logs and customer complaints indicated abnormal behavior.  
2. **Triage:** Security Operations identified the issue and escalated it.  
3. **Analysis:** Firewall logs were reviewed; exploit pattern identified.  
4. **Response:** A custom firewall rule in Python was deployed to block the malicious payload.  
5. **Result:** Service restored, forensic investigation launched.

---

## 🔧 Resolution Steps

- Triage and alert review  
- Log analysis to isolate exploit pattern  
- Rule development using indicators from PoC  
  - [Spring4Shell PoC Reference](https://github.com/craig/SpringCore0day/blob/main/exp.py)  
- Firewall rule deployed  
- Attack traffic blocked  
- Forensics and follow-up actions initiated  

---

## ✅ Action Items

- [x] Deploy permanent firewall rule to block Spring4Shell payload  
- [ ] Share IoCs with internal threat intelligence  
- [ ] Monitor for future variants of similar attacks  
- [ ] Run system-wide scans to ensure no persistence  

---

## 📁 Related Files

- `postmortem.md`: Full incident write-up  
- `firewall-rule.py`: Blocking logic used in firewall  
- `ioc-list.txt`: Indicators of compromise (payload patterns, headers, URLs)

---
