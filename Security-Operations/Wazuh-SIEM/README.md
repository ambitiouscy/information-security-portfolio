
# Wazuh SIEM – Windows Endpoint Monitoring and Detection

## Project Overview

This project documents my hands-on experience deploying and configuring Wazuh as a Security Information and Event Management (SIEM) platform.

The objective was to integrate a Windows endpoint with a Wazuh Manager, collect security events, monitor process creation activity, and develop and test a custom detection rule.

## Lab Environment

| Component | Configuration |
|---|---|
| SIEM Platform | Wazuh 4.13.1 |
| Manager | Linux virtual machine |
| Endpoint | Windows |
| Endpoint Agent | Wazuh Agent |
| Monitoring | Windows Security Event Logs |
| Key Event ID | 4688 – Process Creation |

## Project Activities

### 1. Wazuh Deployment
Installed and configured Wazuh components, including the Manager, Indexer and Dashboard.

### 2. Windows Endpoint Integration
Connected a Windows endpoint to the Wazuh Manager and verified agent communication.

### 3. Security Event Monitoring
Configured and investigated Windows security events, including process creation events (Event ID 4688).

### 4. Command-Line Auditing
Enabled process creation auditing and command-line logging to improve the visibility of executed processes.

### 5. Custom Detection Rule
Developed a custom Wazuh rule (ID 100100) to identify a controlled test command containing the marker `SOC_LAB_TEST`.

### 6. Detection Validation
Performed positive and negative tests to verify that the custom rule matched the intended test activity without matching a different normal test marker.

## Key Findings

- Successfully connected a Windows endpoint to Wazuh.
- Confirmed Windows process creation events were received by Wazuh.
- Captured process names, parent processes and command-line information.
- Successfully validated a custom detection rule using controlled test activity.
- Confirmed that the negative test did not trigger the custom rule.

## Tools and Technologies

- Wazuh SIEM
- Windows Event Viewer
- Windows PowerShell
- Linux
- VirtualBox
- XML

## Project Evidence


The following materials provide evidence of the lab implementation and detection testing:

- [Screenshots](Screenshots/) – Evidence of Wazuh agent connectivity, Windows security event collection, process creation monitoring and custom detection testing.
- [Custom Detection Rule](Detection-Rules/windows_process_creation_rule_100100.xml) – XML configuration for the custom Windows process-creation test detection.
- [SOC Investigation Report](Investigation-Reports/windows-process-creation-investigation.md) – Documentation of the investigation, positive and negative tests, findings and recommendations.


## Learning Outcomes

This project strengthened my practical understanding of endpoint monitoring, security event analysis, SIEM configuration, detection engineering and basic SOC investigation workflows.
