# Incident Postmortem: Malware Attack Leading to NBN Outage

## Summary
- **Incident Start Time:** 2022-03-20T03:16:34Z  
- **Incident End Time:** 2022-03-20T05:16:34Z  
- **Participants:** Telstra Security Operations, NBN team, Networks team  
- **Status:** Resolved  
- **Impact:** Severity 1 - Critical  
- **Detection Time:** 2022-03-20T03:16:34Z  
- **Root Cause Fixed Time:** 2022-03-20T02:16:34Z  

---

## Impact
- Impaired functionality and downtime on NBN services  
- Critical service impact  
- Remote code execution on NBN service infrastructure  

---

## Detection
- Firewall logs notified abnormal activity  
- Impaired functionality and downtime reported via customer complaints  

---

## Root Cause
An attacker exploited the recently released zero-day vulnerability, **Spring4Shell**, targeting the externally exposed **Spring Framework** hosted by the NBN services team.

At **2022-03-20T03:16:34Z**, the attacker launched a **Spring4Shell payload** to perform **remote code execution** on the Telstra NBN network address `nbn.external.network` using HTTP POST requests with malicious query data on the path `/tomcatwar.jsp`.

Firewall alerts and customer complaints revealed the attack and its performance degradation. Forensics confirmed successful remote code execution.

---

## Resolution

- **+30 minutes:**  
  Telstra Security Operations triaged the alert and notified the NBN team about the incident.

- **+60 minutes:**  
  Security Operations analyzed firewall logs and identified a pattern in the malicious requests. This was forwarded to the Networks team.

- **+120 minutes:**  
  The Networks team created and deployed a **firewall rule in Python** to block requests using the Spring4Shell payload (based on this [PoC](https://github.com/craig/SpringCore0day/blob/main/exp.py)).

After deployment, the malware attack was mitigated and NBN services were restored. A forensic process followed.

---

## Action Items
- [ ] Deploy firewall rule to ensure future attacks using this exploit are mitigated  
- [ ] Notify threat intelligence teams to monitor and improve detection of similar payloads  
