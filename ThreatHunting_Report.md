# 🛡️ Threat Hunting Report: PowerShell-Based Port Scan in Azure

## 📌 Overview
This report documents an **observed port scanning activity** originating from `10.0.0.154`, executed via **PowerShell**. The investigation leveraged **Microsoft Defender Advanced Hunting** to identify the source, analyze behavior, and implement mitigation.

---

## 🔍 **Threat Hunting Investigation**

### **Step 1: Identifying Failed Connection Attempts**
- **Query Used:**
  ```kql
  DeviceNetworkEvents
  | where ActionType == "ConnectionFailed"
  | summarize ConnectionCount = count() by DeviceName, ActionType, LocalIP, RemoteIP
  | order by ConnectionCount desc

Findings:
Host 10.0.0.154 attempted multiple failed connections to other hosts.
The failures followed a sequential pattern, suggesting a port scan.

![image](https://github.com/user-attachments/assets/d4045580-0f61-4895-b515-0b4ef2cef1c2)


Step 2: Correlating Process Execution
Query Used:

let IPInQuestion = "10.0.0.154";
DeviceProcessEvents
| where Timestamp between ((datetime(Feb 24, 2025 10:37:22 AM) - 10m) .. (datetime(Feb 24, 2025 10:37:22 AM) + 10m))
| where DeviceName == "lauren-w-sc2"
| order by Timestamp desc
| project Timestamp, FileName, InitiatingProcessCommandLine

Findings:
A suspicious PowerShell script (portscan.ps1) executed under SYSTEM.
Execution time matched the failed connection attempts


![image](https://github.com/user-attachments/assets/d0334598-ef8c-4a65-ab1c-23ecc0fa0eba)


Step 3: Investigating the Host
Action Taken: Logged into 10.0.0.154 and inspected portscan.ps1.
Findings:
The script was configured to scan a subnet for open ports.
Executed using SYSTEM privileges, which is not expected behavior.

![image](https://github.com/user-attachments/assets/8f89849d-92da-4d26-881d-b42d65706d8d)

Step 4: Incident Response
✅ Containment:

Isolated the affected system (10.0.0.154).
Blocked outbound scanning attempts.
✅ Eradication:

Removed portscan.ps1 and checked for persistence.
✅ Recovery:

Reimaged the machine for security assurance.
Applied security patches and reset credentials.
✅ Prevention:

Restricted PowerShell execution:
Set-ExecutionPolicy RemoteSigned -Force

Implemented firewall rules to prevent unauthorized scanning.

🔹 MITRE ATT&CK Mapping
T1046 - Network Service Discovery → Port scanning.
T1059.001 - Command and Scripting Interpreter: PowerShell → Executing portscan.ps1.
T1078 - Valid Accounts → SYSTEM privileges abuse.
T1105 - Ingress Tool Transfer → If the script was downloaded externally.

🎯 Key Takeaways
Used Microsoft Defender Advanced Hunting to detect port scanning.
Identified a PowerShell script (portscan.ps1) running under SYSTEM.
Mapped findings to MITRE ATT&CK (T1046, T1059.001, T1078).
Isolated and reimaged the affected device to ensure security.
Implemented PowerShell restrictions & firewall rules to prevent future incidents.

🔗 Resources
GitHub Repository: [(https://github.com/Lauren-Bitten/Threat-Hunting-Port-Scan)]
LinkedIn Post: [https://www.linkedin.com/feed/update/urn:li:activity:7300008023542956033/]
Cyber Range Discussion: [Insert Cyber Range share link here]

