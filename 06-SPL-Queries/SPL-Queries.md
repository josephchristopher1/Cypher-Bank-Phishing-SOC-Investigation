# SPL Investigation Queries – Cypher Bank Phishing SOC Investigation

This document contains the exact Splunk SPL queries used during the
Cypher Bank phishing-led SOC investigation.  
Each query is mapped to an investigation objective and reflects real
SOC analyst workflows.

---

## 1. Data Presence & Log Health Validation

Purpose: Confirm all required telemetry sources were ingesting data
before investigation began.

```spl
(index=windows OR index=suricata OR index=pfsense)
| stats count by index```

Purpose: Establish a single timeline across endpoint, network, and firewall logs.

```(index=windows OR index=suricata OR index=pfsense)
| timechart span=1m count by index```

Purpose: Identify browser execution consistent with phishing link interaction.

```index=windows sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
(Image="*\\msedge.exe" OR Image="*\\chrome.exe" OR Image="*\\firefox.exe")
| table _time User Image CommandLine ParentImage
| sort _time```

Purpose: Validate outbound network connections originating from browser processes.

```index=windows sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=3
(Image="*\\msedge.exe" OR Image="*\\chrome.exe" OR Image="*\\firefox.exe")
| table _time User DestinationIp DestinationPort Protocol
| sort _time```

Purpose: Confirm whether harvested credentials were used for authentication attempts.

```index=windows (EventCode=4624 OR EventCode=4625)
| table _time User EventCode LogonType Source_Network_Address
| sort _time```

Purpose: Detect post-click payload execution or living-off-the-land activity.

```index=windows sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
(ParentImage="*\\msedge.exe" OR ParentImage="*\\chrome.exe" OR ParentImage="*\\firefox.exe")
(Image="*\\powershell.exe" OR Image="*\\cmd.exe" OR Image="*\\wscript.exe"
OR Image="*\\cscript.exe" OR Image="*\\mshta.exe" OR Image="*\\rundll32.exe"
OR Image="*\\regsvr32.exe" OR Image="*\\certutil.exe" OR Image="*\\bitsadmin.exe")
| table _time User ParentImage Image CommandLine```

Purpose: Identify IDS alerts associated with phishing-related traffic.

```index=suricata
| stats count by src_ip dest_ip proto alert.signature
| sort - count```

Purpose: Inspect HTTP-based phishing communication at the network layer.

```index=suricata proto=http
| table _time src_ip dest_ip http.hostname http.url alert.signature
| sort _time```

Purpose: Confirm allowed traffic paths during the attack window.

```index=pfsense action=pass
| stats count by src_ip dest_ip dest_port proto
| sort - count```

Purpose: Identify denied or blocked connections related to phishing infrastructure.

```index=pfsense (action=block OR action=deny)
| stats count by src_ip dest_ip dest_port proto
| sort - count```

Purpose: Correlate endpoint, IDS, and firewall evidence into a single view.

```(index=windows OR index=suricata OR index=pfsense)
| table _time index User src_ip dest_ip DestinationIp DestinationPort Image alert.signature action
| sort _time```

Purpose: Pivot investigation around a specific victim user or IP address.

```(index=windows OR index=suricata OR index=pfsense)
(User="VICTIM_USER" OR src_ip="VICTIM_IP" OR dest_ip="VICTIM_IP")
| table _time index User src_ip dest_ip DestinationIp DestinationPort Image alert.signature
| sort _time
```





