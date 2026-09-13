# Data Flow
## Purpose
This Document describes the primary network communication paths within JangoNet Environment. This includes source systems, destination systems, required protocols, security controls, and expected behavior.

## Architecture Diagram

<img width="1006" height="847" alt="image" src="https://github.com/user-attachments/assets/59b7ecd5-9d2f-46ad-a6a3-428a7da81c16" />

## Network Zones

- Management: 192.168.10.0/24
- Users: 192.168.20.0/24
- Servers: 192.168.30.0/24
- WAN: External/Internet

  **Management:** This network segment contains highly privileged devices that provide administrators with secure shell and remote desktop access to         critical systems. These devices serve as jump boxes for administrators and are subject to stricter security policies.

  **Users:** This network segment contains user devices that are domain joined. These devices are subject to standard security policies.

  **Servers:** This network segment contains critical devices for the network, including: Domain Controller, File Server, and a Security Information Event   Manager.

## Active Directory authentication flow

  **Source:**
  
    -User Subnet
    
    -Management Subnet

  **Destination:**
    -JANGO_DC1

**Purpose:** 

  Allow domain-joined clients to locate the domain controller, authenticate users, process group policy, and access AD services

**Needed Protocols:**
Service:

DNS            TCP/UDP    53            Locate DC and AD services

Kerberos       TCP/UDP    88            Domain Authentication

LDAP           TCP/UDP    389           Directory Queries

SMB            TCP        445           SYSVOL/NETLOGON/GPO

RPC            TCP        135           RPC endpoint mapping

Dynamic RPD    TCP        49152-65535   AD/Windows RPC Operations

Kerberos PWC   TCP/UDP    464           Password Changes


## DNS Resolution Flow

DNS Queries  ->  JANGO_DC  -> Upstream Resolver

## DHCP Flow

DHCP Server: JANGO_DC1

Scope: 192.168.10.0/24   Available: 192.168.10.0/25

**Needed Protocols:**

DHCP server/relay    UDP    67

DHCP client          UDP    68

**Note:**

  pfSense serves as DHCP relay on users interface, pointing to JANGO_DC1
  
  <img width="1138" height="445" alt="image" src="https://github.com/user-attachments/assets/bb72a79b-21d6-46fc-b5fa-5c0c2db6a535" />


