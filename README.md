# 🔍 Threat Hunting: Detecting PowerShell-Based Port Scanning in Azure

## 📌 Overview
This project is a real-world **threat hunting case study**, investigating **PowerShell-based port scanning in an Azure environment**. The analysis leverages **Microsoft Defender Advanced Hunting** to track suspicious activity, correlate events, and map to **MITRE ATT&CK techniques**.

## 🚀 Key Findings
- **Identified failed connections** that indicated potential **port scanning**.
- Correlated logs and found a **PowerShell script (`portscan.ps1`)** executed under SYSTEM.
- Mapped findings to **MITRE ATT&CK techniques**:
  - **T1046** - Network Service Discovery
  - **T1059.001** - PowerShell Execution
  - **T1078** - Valid Accounts

## 📂 Project Files
- **📄 ThreatHunting_Report.md** – Full threat hunting report & findings  
- **📜 queries.kql** – KQL queries used for detection  
- **💻 portscan.ps1** – The PowerShell script used for scanning  
- **📸 screenshots/** – Screenshots from the investigation  

## 🔹 MITRE ATT&CK Mapping
- **T1046 - Network Service Discovery** → Port scanning to identify open services.  
- **T1059.001 - Command and Scripting Interpreter: PowerShell** → Execution of a PowerShell script.  
- **T1078 - Valid Accounts** → SYSTEM privilege abuse.  

## 🏆 Lessons Learned
- How to **identify malicious port scans** in cloud environments.  
- Effective use of **Microsoft Defender Advanced Hunting** queries.  
- The importance of **incident response & security hardening**.

## 📢 Want to Collaborate?
Feel free to **fork this repo**, contribute, or reach out for discussions! 🚀  
