#   Cypher Bank – Phishing-Led SOC Investigation

---

##   Project Overview

This repository documents a complete, end-to-end **Security Operations Centre (SOC)** investigation of a phishing-led attack simulation conducted against a fictional financial institution, **Cypher Bank Limited**.

The project mirrors real-world SOC investigation practices used in regulated financial environments and demonstrates how a SOC analyst detects, correlates, investigates, and validates phishing incidents using **Splunk SIEM** and multi-source security telemetry.

The investigation focuses on **detection, validation, and incident scoping**, rather than exploitation, to reflect professional SOC workflows.

A full written investigation report is provided as a PDF and aligns directly with this README.

---

##   SOC Architecture & Telemetry Overview

The investigation was conducted within a controlled SOC lab environment designed to simulate enterprise-grade security monitoring.

### Telemetry Sources

**Windows Endpoint Telemetry**
- Collected via **Sysmon**
- Process creation, command-line execution, user context, and network activity

**Network & Firewall Logs**
- Collected via **pfSense**
- Egress traffic visibility and firewall event monitoring

**Intrusion Detection**
- Collected via **Suricata IDS**
- HTTP requests, DNS queries, and protocol-level inspection

**Email Telemetry**
- Collected via **hMailServer** and **GoPhish**
- Email delivery, phishing campaign execution, and user interaction tracking

A full architecture diagram is available in:
`02-Project-Architecture/`

---

##   Attack Simulation Summary

The phishing simulation was intentionally scoped to prioritise **SOC investigation and validation**, rather than attacker exploitation.

Observed activity included:

- Phishing email delivered to internal Cypher Bank mailboxes
- User interaction observed (email opened and phishing link clicked)
- Credential harvesting page accessed
- No malware payload execution detected
- No lateral movement observed
- No endpoint compromise identified

The simulation was intentionally stopped at credential harvesting to maintain focus on SOC investigation, validation, and scoping workflows.

---

##   Investigation Methodology

The investigation followed a structured **Security Operations Centre (SOC)** methodology aligned with real-world blue team practices.

The objective was to validate a phishing-led attack through **evidence-based correlation**, ensuring no alert or telemetry source was analysed in isolation.

### SOC Workflow Phases

- Detection  
- Triage  
- Correlation  
- Investigation  
- Response  
- Review  

Email telemetry was analysed first to confirm phishing delivery and user interaction. Findings were then correlated with endpoint and network telemetry within defined time windows to validate attacker activity and eliminate false positives.

All analysis was conducted using **manual correlation**, reflecting environments without SOAR automation while remaining automation-ready for future scaling.

---

##   Artifacts & Evidence Analysis

Multiple forensic artifacts were identified and validated across email, endpoint, and network telemetry sources.

### Key Artifacts Reviewed

- Phishing URLs accessed by affected users identified via **Suricata HTTP logs** and **DNS queries**
- Source and destination IP addresses associated with outbound connections
- Ports and protocols (e.g. **TCP 443**, **DNS 53**) confirming encrypted outbound communication
- Email sender domain and internal sender identity validated via **mail server logs**
- Endpoint execution evidence from **Sysmon**, including process creation and network activity

All artifacts were validated through **cross-correlation in Splunk**, ensuring accuracy and preventing reliance on a single alert or data source.

Evidence screenshots are located in:
`04-Evidence-Screenshots/`

---

##   Response & Mitigation Actions

Upon confirmation of credential harvesting activity, the following response actions were executed:

- Impacted user accounts secured and credentials reset
- Active sessions revoked to prevent unauthorised access
- Email activity reviewed for forwarding rules or mailbox abuse
- Endpoint telemetry validated to confirm **no malicious payload execution**
- Continued monitoring enabled for affected users and associated IP addresses
- Phishing awareness reinforcement conducted

No evidence of lateral movement or post-exploitation activity was observed.

---

##   Mitigation & Hardening Measures

Post-incident mitigation focused on reducing both likelihood and impact of future phishing attempts:

- Enforcement of **Multi-Factor Authentication (MFA)** using conditional access controls
- Improved SOC visibility through tighter correlation across email, endpoint, and network telemetry
- Reinforced user awareness around phishing identification and reporting
- Validation of endpoint integrity following credential exposure
- Refinement of detection dashboards and verification of logging coverage

These measures strengthened both **preventive** and **detective** security controls.

---

##   Lessons Learned & Recommendations

Key lessons identified during the investigation align with **NIST Cybersecurity Framework (CSF)** principles:

- **Identify:** Comprehensive telemetry visibility is critical for accurate investigations
- **Protect:** MFA significantly reduces credential abuse risk
- **Detect:** Multi-source correlation increases investigative confidence
- **Respond:** Rapid containment prevents escalation
- **Recover:** Monitoring and process refinement close the incident response loop

### Recommendations

- Implement enterprise email authentication (**SPF, DKIM, DMARC**)
- Enforce MFA for email and remote access
- Formalise SOC incident response playbooks and escalation procedures
- Enhance automated alert correlation to reduce **MTTR**

---

##   MITRE ATT&CK Mapping

Observed activity was mapped to the **MITRE ATT&CK** framework to align findings with industry-standard threat classification:

- **T1566** – Phishing  
- **T1071.004** – Application Layer Protocol (HTTP)

Full mapping is available in:
`05-IOCs-and-MITRE/`

---

##   SPL Queries & Investigation Searches

All Splunk searches used during the investigation are fully documented in:

`06-SPL-Queries/SPL-Queries.md`

These queries support validation, correlation, and evidence generation.

---

##   Disclaimer

This project was conducted in a controlled lab environment using fictional entities.

No real organisation, users, or production systems were involved.
