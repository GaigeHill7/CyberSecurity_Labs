# Microsoft Sentinel Privilege Escalation Detection

## Description
Deployed a Microsoft Sentinel privilege escalation detection rule by ingesting Windows Security Events into Log Analytics and using KQL to identify Event ID 4732, which indicates a user being added to a privileged group. Configured a Sentinel automation rule to automatically create and assign incidents to the appropriate operator for investigation.

## Features
**Vulnerable VM Deployment** - Provisioned a windows virtual machine on Azure

**Log Ingestion** - Collected and forwarded windows security event logs from the VM into microsoft sentinel via a DCR

**KQL Querying** - Used KQL to parse and filter security events (EventID = 4732)

**Custom Analytic Rule** - Parses the event using KQL and automatically creates incident for investigation

**Automation Rule** - Incident gets automatically assigned and notifies operator of incident alert

## Results
Succesfully created a rule to trigger an incident event in Microsoft Sentinel when priviledge escalation is detected on device

## Analytics Rule 
SecurityEvent
| where EventID == 4732
| where TargetAccount =="Builtin\\Administrators"
<img width="1418" height="423" alt="image" src="https://github.com/user-attachments/assets/7ac691de-6d25-44f5-b543-35a4810abfd4" />

## Incident Creation 
<img width="1094" height="818" alt="image" src="https://github.com/user-attachments/assets/981c08ba-ea15-47d4-b701-e2ac24090ad1" />

