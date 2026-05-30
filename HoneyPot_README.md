# Microsoft Sentinel Honey Pot

## Description
Deployed a cloud-based honeypot on Microsoft Azure using a deliberately vulnerable virtual machine to attract and capture malicious activity. Collected and ingested security logs into Microsoft Sentinel, where I built a custom workbook to visualize and analyze attack data in real time.

## Features
**Vulnerable VM Deployment** - Provisioned a windows virtual machine on Azure, configured to attract real-world attacks

**Exposed Attack Surface** - Disabled firewall rules to allow inbound traffic from the internet, simulating a vulnerable machine

**Log Ingestion** - Collected and forwarded windows security event logs from the VM into microsoft sentinel via a DCR

**KQL Querying** - Used KQL to parse and filter security events (EventID = 4265)

**Custom Sentinel Workbook** - Built an interactive dashboard to visualize attack data including login attempts, source IPs, and geographic origin

## Results
In 45 mins the vulnerable machine recieved over 500 brute force attempts from over 8 different IPs across the world. This lab emphazied the importance of hardening vulnerable devices from attacks, and the undenying threat of cybersecurity attacks

## Sentinel Workbook
https://security.microsoft.com/sentinel/926df020-464d-45cb-be02-44dc0ac1fe5c/soc-lab/soc-lab-law/workbook/%2Fsubscriptions%2F926df020-464d-45cb-be02-44dc0ac1fe5c%2Fresourcegroups%2Fsoc-lab%2Fproviders%2Fmicrosoft.insights%2Fworkbooks%2Fd94f713d-f011-4408-8df6-55087fd15196?tid=3bd6eff5-3688-4f79-8a71-f55c4a220771&wbViewMode=readonly 

## Lab Diagram
<img width="970" height="553" alt="SIEM_LAB drawio" src="https://github.com/user-attachments/assets/6579bb25-c336-456e-9d23-f55b1f62e466" />

