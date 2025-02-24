# Threat Hunting: Detecting Port Scans in Azure

## 📌 Overview
This project is a hands-on **threat hunting investigation** using **Microsoft Defender Advanced Hunting** to detect **PowerShell-based port scanning** in an Azure environment.

### 🔍 Key Findings:
- Identified failed connections suggesting a **port scan**.
- Correlated logs using **DeviceNetworkEvents & DeviceProcessEvents**.
- Found a suspicious **PowerShell script (`portscan.ps1`)** executed under SYSTEM.
- Mapped findings to **MITRE ATT&CK**:  
  - 🛠 **T1046** - Network Service Discovery  
  - 🛠 **T1059.001** - PowerShell Execution  
  - 🛠 **T1078** - Valid Accounts Misuse

### 🚀 What’s Included:
- **📄 ThreatHunting_Report.md** – Full analysis & notes
- **📜 queries.kql** – KQL queries used for detection
- **💻 portscan.ps1** – The PowerShell script used for scanning
- **📸 screenshots/** – Evidence from the investigation

## 🏆 Lessons Learned
- How to **identify malicious port scans** in cloud environments.
- Effective use of **Microsoft Defender Advanced Hunting**.
- Importance of **incident response** in a SOC workflow.

## 📢 Want to Collaborate?
Feel free to fork this repo, contribute, or reach out with suggestions!
