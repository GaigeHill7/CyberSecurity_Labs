# Elastic Dashboards

## Failed Login Attempts
Developed a security dashboard to visualize failed login attempts to quickly detect suspicious activity
Filter = event.code : 4625
Relevant Windows Event ID : 4625 (Failed Authentication attempts)
Included Fields: user.name.keyword, host.hostname.keyword, winlog.logon.type.keyword
<img width="934" height="649" alt="image" src="https://github.com/user-attachments/assets/3fb32856-0ab4-4938-9cdc-6f8b450b6673" />


