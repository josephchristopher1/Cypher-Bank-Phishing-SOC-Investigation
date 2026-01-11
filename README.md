# Cypher Bank – Phishing-Led SOC Investigation

## Project Overview
This project documents an end-to-end SOC investigation of a phishing-led attack against a fictional financial institution, **Cypher Bank Limited**.  
The simulation replicates real-world email-based threats and demonstrates how a SOC analyst detects, correlates, investigates, and validates a phishing incident using SIEM and security telemetry.

The objective was to identify user interaction with a phishing email, validate endpoint and network activity, and confirm whether credential harvesting or post-click execution occurred.

---

## SOC Architecture & Telemetry
The investigation is supported by a controlled SOC lab environment with centralised logging and correlation in **Splunk SIEM**.

**Telemetry sources include:**
- Windows endpoint telemetry via **Sysmon**
- Network traffic and firewall logs via **pfSense**
- IDS alerts via **Suricata**
- Email delivery and interaction via **hMailServer** and GoPhish

📄 Full architecture diagram:  
`02-Project-Architecture/Joseph-Cypher Bank Project-Architectural design.pdf`

---

## Attack Simulation Summary
- Phishing email delivered to internal Cypher Bank users
- User interaction observed (email open and link click)
- Credential harvesting page accessed
- No malware payload execution detected
- No lateral movement or endpoint compromise observed

The simulation intentionally stopped at credential harvesting to focus on investigation and validation workflows rather than exploitation.

---

## Investigation Workflow
The SOC investigation followed a structured, analyst-driven workflow:

1. Validation of log ingestion and data health  
2. Timeline reconstruction across endpoint and network logs  
3. Endpoint process analysis using Sysmon events  
4. Network traffic inspection via Suricata and pfSense  
5. Authentication attempt analysis for harvested credentials  
6. Evidence correlation and incident scoping

All investigation queries used during this process are documented in:
`06-SPL-Queries/SPL-Queries.md`

---

## MITRE ATT&CK Mapping
Observed techniques were mapped to the MITRE ATT&CK framework to align findings with industry standards.

- **T1566** – Phishing  
- **T1071.004** – Application Layer Protocol (HTTP)

Full mapping available in:
`05-IOCs-and-MITRE/MITRE-Mapping.md`

---

## Evidence & Dashboards
Screenshots included in this repository represent validated investigation evidence:
- SOC phishing overview dashboard
- Endpoint process creation events
- Network and IDS correlation
- Email interaction confirmation

Evidence screenshots are located in:
`04-Evidence-Screenshots/`

---

## Outcome & SOC Assessment
- Phishing attack detected and investigated successfully
- Credential harvesting confirmed
- No post-click execution or lateral movement identified
- Incident contained through investigation and validation

This project demonstrates **SOC Level 2 investigation capability**, including log correlation, threat validation, MITRE mapping, and professional incident documentation.

---

## Disclaimer
This project was conducted in a controlled lab environment using fictional entities.  
No real organisation, users, or production systems were involved.
