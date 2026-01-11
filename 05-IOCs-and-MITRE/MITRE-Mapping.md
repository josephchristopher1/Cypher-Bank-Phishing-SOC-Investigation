
## MITRE ATT&CK Mapping – Cypher Bank Phishing Simulation

### ATT&CK Techniques Observed
- T1566 – Phishing
- T1071.004 – Application Layer Protocol (HTTP)

### Techniques Investigated but Not Observed
- T1059 – Command and Scripting Interpreter

### Evidence Sources
- GoPhish campaign tracking (email sent, opened, link clicked)
- Splunk correlation searches
- User mailbox interaction screenshots

### SOC Response Metrics
- Mean Time To Detect (MTTD): Within minutes of user interaction
- Mean Time To Respond (MTTR): Same investigation window (no escalation required)

### Analyst Notes
This phishing simulation intentionally stopped at credential harvesting.
No malware payload execution or endpoint compromise was observed.
Containment was achieved through investigation and validation.
