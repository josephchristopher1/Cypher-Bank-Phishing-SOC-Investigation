Cypher Bank – Phishing-Led SOC Investigation
Project Overview

This repository documents a complete, end-to-end Security Operations Centre (SOC) investigation of a phishing-led attack simulation conducted against a fictional financial institution, Cypher Bank Limited.

The project mirrors real-world SOC investigation practices used in regulated financial environments and demonstrates how a SOC analyst detects, correlates, investigates, and validates phishing incidents using Splunk SIEM and multi-source security telemetry.

The investigation focuses on detection, validation, and incident scoping, rather than exploitation, to reflect professional SOC workflows.

A full written investigation report is provided as a PDF and aligns directly with this README.

SOC Architecture & Telemetry Overview

The investigation was conducted within a controlled SOC lab environment designed to simulate enterprise-grade security monitoring.

Telemetry Sources

Windows Endpoint Telemetry

Collected via Sysmon

Process creation, command-line execution, and user context

Network & Firewall Logs

Collected via pfSense

Egress traffic and firewall visibility

Intrusion Detection

Alerts generated via Suricata IDS

Email Infrastructure

Internal mail delivery via hMailServer

Phishing campaign orchestration via GoPhish

Central SIEM

All telemetry aggregated, correlated, and investigated in Splunk SIEM

Full architecture diagram and explanation available in:
02-Project-Architecture/Joseph-Cypher Bank Project-Architectural design.pdf

Attack Simulation Summary

The simulated attack replicated a realistic phishing scenario targeting internal Cypher Bank users.

Phishing email delivered to internal Cypher Bank mailboxes

User interaction observed (email opened and link clicked)

Credential harvesting page accessed

No malware payload execution detected

No lateral movement observed

No endpoint compromise identified

The simulation was intentionally stopped at credential harvesting to prioritise SOC investigation, validation, and scoping workflows.

Investigation Methodology

The SOC investigation followed a structured, analyst-driven workflow, aligned with SOC Level 2 operational practices.

Investigation Steps

Validation of log ingestion and data health across all telemetry sources

Timeline reconstruction across endpoint, network, and email logs

Endpoint process analysis using Sysmon process creation events

Network traffic and IDS alert inspection using Suricata and pfSense

Authentication attempt analysis for harvested credentials

Evidence correlation and incident scoping

All Splunk searches used during this investigation are documented in:
06-SPL-Queries/SPL-Queries.md

MITRE ATT&CK Mapping

Observed activity was mapped to the MITRE ATT&CK framework to align findings with industry-standard threat classification.

Techniques Observed

T1566 – Phishing

T1071.004 – Application Layer Protocol (HTTP)

Full MITRE mapping and IOC documentation available in:
05-IOCs-and-MITRE/MITRE-Mapping.md

Evidence & Dashboards

This repository includes validated investigation evidence captured directly from Splunk during the investigation.

Included Evidence

SOC phishing investigation overview dashboard

Endpoint process creation events (Sysmon Event ID 1)

Network and IDS correlation results

Email delivery and user interaction confirmation

Evidence screenshots are located in:
04-Evidence-Screenshots/

Mitigation Actions

Based on the investigation findings, the following mitigation actions were identified and applied:

Incident contained through investigation and validation

No endpoint isolation required due to absence of compromise

No password resets required due to lack of authentication attempts

Phishing campaign terminated after confirmation of user interaction

Incident documented and closed following SOC procedures

Lessons Learned

Phishing remains an effective initial access vector

User interaction does not automatically result in endpoint compromise

Centralised telemetry enables rapid incident validation

Early investigation reduces operational and security impact

Clear separation between detection and exploitation improves SOC realism

Recommendations

Strengthen phishing awareness training for internal users

Enhance email filtering and phishing detection controls

Monitor for delayed credential misuse post-incident

Expand automated correlation rules for phishing indicators

Conduct regular SOC readiness simulations

Outcome & SOC Assessment

Phishing activity successfully detected and investigated

Credential harvesting activity confirmed

No post-click execution or lateral movement identified

Incident contained through structured SOC investigation

Demonstrates SOC Level 2 investigation capability

Supporting Documentation

Full Investigation Report (PDF)
SOC_SPL_Wall_Sheet_FULL_Thorough_Investigation_Correlation_A4.pdf

SOC Architecture Diagram (PDF)
02-Project-Architecture/Joseph-Cypher Bank Project-Architectural design.pdf

Disclaimer

This project was conducted in a controlled lab environment using fictional entities.
No real organisations, users, or production systems were involved.
