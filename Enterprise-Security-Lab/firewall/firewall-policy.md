# Firewall Policies
## Purpose
This firewall policy enforces least-privilege by applying a default deny structure. It is aligned with NIST 800-41 publication to create the most secure environment possible. 

## Security Principles Applied:

1. Deny traffic by default
2. Establish host and network aliases.
3. Permit only explicitly authorized traffic.
4. Apply least-privilege access by only allowing necessary traffic through firewall.
5. Separate user, administrative, server, and management traffic.
6. Require administrators to access critical systems through approved jump boxes.
7. Restrict inbound internet traffic unless specifically required.

## Permitted Traffic

Traffic may be permitted when it supports an approved operational or security requirement

Examples included:
- User devices accessing DNS and DHCP services
- Domain-joined systems communicating with domain controllers
- Approved outbound web traffic
- Administrative jump boxes connecting to managed servers
- Systems forwarding security logs to the SIEM
- Management stations connecting to infrastructure interfaces
- Approved update and vulnerability-management traffic

# Reference Images
## WAN Interface

<img width="1138" height="191" alt="image" src="https://github.com/user-attachments/assets/fc85b5e0-184c-44e5-b283-01dbca674ebb" />

## Management Interface

<img width="1140" height="950" alt="image" src="https://github.com/user-attachments/assets/dc05428c-30d6-4274-965f-f7c33e956611" />

## Users

<img width="1137" height="1101" alt="image" src="https://github.com/user-attachments/assets/483d1f61-d81a-471b-8ad4-0b2a3eb391b3" />

## Servers

<img width="1139" height="620" alt="image" src="https://github.com/user-attachments/assets/ddedac6d-9fb0-47c9-bbc7-77fb5aec218e" />

