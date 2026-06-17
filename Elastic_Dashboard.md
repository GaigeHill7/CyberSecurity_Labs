# Elastic Dashboards

## 1) Failed Login Attempts
Developed a security dashboard to visualize failed login attempts to quickly detect suspicious activity

**Filter** = event.code : 4625

**Relevant Windows Event ID** : 4625 (Failed Authentication attempts)

**Included Fields**: user.name.keyword, host.hostname.keyword, winlog.logon.type.keyword

<img width="934" height="649" alt="image" src="https://github.com/user-attachments/assets/3fb32856-0ab4-4938-9cdc-6f8b450b6673" />

## 2) Disabled accounts due to failed login attempts
Developed a security dashboard to visualize user accounts who have been disable due to failed login attempts

**Filter** = event.code : 4625 AND winlog.event_data.SubStatus:0xC0000072

**Relevant Windows Event ID** : 4625 (Failed Authentication attempt)

**Included Fields** : user.name.keyword, host.hostname.keyword

<img width="704" height="98" alt="image" src="https://github.com/user-attachments/assets/4c744e09-a829-4c41-bebd-d7ef006de917" />
