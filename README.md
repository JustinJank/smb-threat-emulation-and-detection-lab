# SMB Attack Emulation & PowerShell IDS Detection Lab

## Detection Engineering • Windows Telemetry • MITRE ATT&CK Mapping

---

## Project Overview

This project simulates a realistic **SMB-based attack chain in a controlled Windows lab environment** and demonstrates how blue team detection engineering can identify and respond to reconnaissance activity.

The lab emulates attacker behavior using **Nmap driven network scanning as well as SMB enumeration**, then applies a custom **PowerShell based Intrusion Detection System (IDS)  script** to automatically detect suspicious network activity in real time.

All activity is analyzed using **Windows Event Logs, Sysmon telemetry, and Firewall logging**, and mapped to the MITRE ATT&CK framework.

---

## Core Objectives

- Simulate SMB reconnaissance and enumeration behavior using Nmap  
- Capture and analyze Windows Security, Sysmon, and Firewall logs  
- Observe attacker based network scanning patterns  
- Code and deploy a PowerShell based IDS for real time detection  
- Correlate telemetry across multiple Windows logging sources  
- Map attacker behavior to MITRE ATT&CK techniques  

---

## Security Stack Used

- Windows Event Viewer (Security Logs)  
- Sysmon (process creation, network connections, and system telemetry)  
- Windows Firewall Logging  
- Native Windows network monitoring tools  
- PowerShell based IDS (custom detection script)  
- Nmap (attack simulation and reconnaissance tool)  

---

# Attack Lifecycle Overview

The simulation follows a structured attack flow:

> Reconnaissance → Service Discovery → SMB Enumeration → Authentication Attempts → Telemetry Collection → Detection → Alerting

Each stage was personally documented through screenshots to assist in representing the full attack to detection pipeline.

---

#  Attack Timeline & Evidence

---

 Phase 1 — SMB Service Exposure & Environment Setup

### SMB Initialization & Accessibility Validation

<img width="2132" height="984" alt="Enabling_SMB_and_Nmap_of_Services_1" src="https://github.com/user-attachments/assets/3ad6a79a-0bcf-4a2a-9053-ddf75c5b5797" />
<img width="995" height="936" alt="Enumerating_SMB_2" src="https://github.com/user-attachments/assets/4671d1f6-7ce5-488f-a244-0e12afb5de98" />

The environment is configured with SMB services enabled to simulate an exposed Windows network service. Initial validation confirms accessibility over port 445.

**MITRE ATT&CK:**
- T1046 – Network Service Scanning  
- T1135 – Network Share Discovery  

---

## Phase 2 — Reconnaissance (Nmap Scanning)

### Active Network Scanning via Nmap

<img width="2443" height="1383" alt="Nmap_Defense_Logging_3" src="https://github.com/user-attachments/assets/64e2fee0-5c53-428a-bd9e-3431710b6a98" />
<img width="1021" height="847" alt="Windows_Endpoint_Telemetry_Sysmon_4" src="https://github.com/user-attachments/assets/3db2860a-4fab-47d4-af9b-d87ad49e2904" />
<img width="2530" height="1439" alt="Security_Logs_Success_SMB_Attack_Login_5" src="https://github.com/user-attachments/assets/f2771fa0-51ba-4dd8-9613-a4b6fcc7f85d" />

The attacker simulation begins with Nmap scanning to identify open ports, services, and SMB exposure.

**MITRE ATT&CK:**
- T1046 – Network Service Scanning  
- T1595 – Active Scanning  

---

## Phase 3 — SMB Enumeration & Access Attempts

### Share Enumeration & Authentication Activity

<img width="2530" height="1439" alt="Security_Log_Failed_SMB_Attack_Login_6" src="https://github.com/user-attachments/assets/cf734cae-b22d-47b2-83c4-fe4d8343deff" />
<img width="2513" height="1439" alt="Security_Log_Showing_Attacker_Info_7" src="https://github.com/user-attachments/assets/4b5d13d4-97b8-4317-87a5-67ecbae2716d" />
<img width="1016" height="851" alt="Security_Log_Failed_Signon_Cont_8" src="https://github.com/user-attachments/assets/21698d72-f36b-4855-a6c5-c84f1ed0658e" />
<img width="1013" height="848" alt="Filtered_Logon_Results_9" src="https://github.com/user-attachments/assets/3c02ebf4-7ee5-4a1b-9b2b-c339d939e03e" />

SMB shares are enumerated and authentication attempts are observed. Windows Security logs capture failed login attempts and suspicious access behavior.

**MITRE ATT&CK:**
- T1135 – Network Share Discovery  
- T1110 – Brute Force  
- T1078 – Valid Accounts (if successful authentication occurs)  

---

## Phase 4 — Log Collection & Telemetry Correlation

### Security Log & Sysmon Analysis

<img width="842" height="679" alt="XML_Data_Successful_Attack_Logon_10" src="https://github.com/user-attachments/assets/80da879b-b16e-468b-a9a1-e04603c48aca" />
<img width="1005" height="736" alt="XML_Data_Cont_11" src="https://github.com/user-attachments/assets/caf1c088-fd3b-4e02-8a88-5564b1655a1f" />
<img width="1008" height="768" alt="Enabling_Firewall_Logging_12" src="https://github.com/user-attachments/assets/edc901a9-b355-4549-a5db-c14d172584f5" />

Windows Security logs and Sysmon telemetry are analyzed to correlate process execution, network connections, and authentication events.

Sysmon provides enhanced visibility into:
- Process creation events  
- Network connection telemetry  
- System level activity correlation  

**MITRE ATT&CK:**
- T1005 – Data from Local System  
- T1046 – Network Service Scanning (correlated activity)  

---

##  Phase 5 — Firewall Logging & Network Visibility

### Firewall Telemetry Activation

<img width="1014" height="760" alt="Firewall_Log_File_PS_13" src="https://github.com/user-attachments/assets/bd1cfb7b-652c-4e13-a207-fbe68b1dcb1d" />
<img width="997" height="885" alt="Nmap_Auto_Detection_Script_via_PS_14" src="https://github.com/user-attachments/assets/00790f07-1fd7-4671-99e3-2bdfae07ddb2" />

Windows Firewall logging is enabled to capture inbound and outbound connection attempts, improving visibility into scanning behavior.

**MITRE ATT&CK:**
- T1040 – Network Sniffing (observational context)  
- T1046 – Network Service Scanning  

---

## Phase 6 — PowerShell IDS Deployment
### Real Time Detection Engine Activation

<img width="989" height="767" alt="IDS_Script_Creation_15" src="https://github.com/user-attachments/assets/f116abe6-25e9-4806-81dd-96c49e0759ba" />
<img width="1014" height="828" alt="Successful_IDS_Script_Creation_16" src="https://github.com/user-attachments/assets/dccedcc7-2307-4dd0-86ff-b81455ad394a" />
<img width="2145" height="1373" alt="Final_nmap_scan_and_results_16" src="https://github.com/user-attachments/assets/40a98803-5b15-4537-b4fe-c0c1245efcf4" />

A custom PowerShell based IDS is deployed to passively and automatically monitor active network connections to detect reconnaissance behavior, such as rapid port scanning and repeated SMB access attempts.

**MITRE ATT&CK:**
- T1059.001 – PowerShell Execution  
- T1046 – Network Service Scanning  

---

##  Phase 7 — Detection & Alerting

### IDS Detection Triggered

<img width="2512" height="1437" alt="IDS_Log_Results_Confirming_Nmap_Scans_And_IPs_16" src="https://github.com/user-attachments/assets/8b091ec0-78c6-4c6d-a2b4-1bb4d07c30df" />
<img width="2454" height="1384" alt="IDS_Log_Real_Time_Detections_17" src="https://github.com/user-attachments/assets/28e5ce91-660b-4bbb-a743-83f0858f60ca" />

The IDS successfully identifies scanning behavior consistent with Nmap reconnaissance and logs a real-time alert for further investigation.

**MITRE ATT&CK:**
- TA0007 – Discovery  
- T1046 – Network Service Scanning  

---

#  MITRE ATT&CK Summary of Relevance

| Technique ID | Technique | Detection Source |
|--------------|----------|------------------|
| T1046 | Network Service Scanning | PowerShell IDS + Firewall + Sysmon |
| T1135 | Network Share Discovery | Security Logs |
| T1110 | Brute Force | Authentication Logs |
| T1078 | Valid Accounts | Security Logs |
| T1059.001 | PowerShell | IDS Execution |
| T1005 | Data from Local System | Log Analysis |
| T1595 | Active Scanning | Nmap Simulation |
| T1040 | Network Sniffing (contextual visibility) | Firewall + Sysmon telemetry |

---

#  PowerShell IDS Summary

The PowerShell based IDS functions as a lightweight detection engine that continuously monitors active network connections and flags suspicious behavioral patterns, including:

- Rapid connection attempts from a single source IP  
- Repeated SMB (port 445) scanning activity  
- Network behavior consistent with reconnaissance tools such as Nmap  

All detections are logged for forensic review and SOC style analysis.

---

#  Key Findings

- SMB services can be easily discoverable through basic network scanning techniques  
- Sysmon significantly enhances endpoint visibility (process + network telemetry)  
- Windows Security Logs provide strong authentication and access tracking  
- Firewall logging improves network level detection coverage  
- Simple PowerShell logic can effectively detect early stage reconnaissance behavior  
- Cross source correlation (Security + Sysmon + Firewall) improves detection accuracy  

---

#  Future Potential Improvements

- SIEM integration (Splunk, Microsoft Sentinel, ELK Stack)  
- Rule based detection engine expansion (modular IDS design)  
- Behavioral anomaly scoring for scan detection  
- Automated alerting via webhook or email  
- Expanded MITRE ATT&CK coverage (lateral movement, persistence, execution chains)  

---

#  Disclaimer

This project was conducted in a controlled lab environment for educational and cybersecurity research purposes only.

If you choose to replicate these steps in your own home lab, ensure that your environment has been properly air gapped or fully isolated from production networks to prevent unintended network exposure or unauthorized access.
