# Analyzing Evil with Sysmon & Event Logs

## Overview
This lab covers a Hack The Box practical demonstrating advanced detection techniques using **Sysmon** and **Windows Event Viewer**. These tools and processes allow analyst to identify and investigate suspicous behaviors and attack techniques such as DLL hijacking, Powershell/C# injection, and credential dumping (mimikatz).

## Key Concepts
- **Sysmon** is a windows telemetry tool that gives deep visibility into what processes, files, DLLs, registry keys, and monitor network connection.
- **IOCs** (Indicators of Compromise) is a inidicator of a potential attack or infection on a system
- **Attack Techniques Covered:**
    - DLL Hijacking
    - PowerShell Injection
    - Credential Dumping (via LSASS)
---
## DLL Hijacking
DLL Hijacking is an exploit on windows applications which load linked libraries on execution. A Windows program relies on these DLLs to function as intended, if they're unable to find their linked library, they can't perform their desired action. Attackers exploit the order of which the programs search for their linked libraries by placing malicous code early in their search order, forcing the application to run their arbitirary code. Some application run at system level priviledges, if able to hijack this applications DLL, they can run their code at the same level priviledge.

  **Exploit**
  
    1. Gain access to user device
    
    2. Using Process Monitor, determine where the application is looking for its DLLs
    
    3. Place the malicous DLL file earlier in its search order

  **Risks**
  
    1. Run arbitrary code
    
    2. Bypass security controls
    
    3. Establish persistence
    
    4. Credential harvesting

  **Detection**
  
    1. Detect if a process is loading a DLL from an unusual location
    
    2. Check for valid signature

  **Mitigations**
  
    1. Use safe DLL search settings. Helps restrict where the applications load DLLs from
    
    2. Remove writing permissions to application folders
    
    3. Block unknown or untrusted DLLs

## DLL Hijacking Lab:

1. Create a copy of calc.exe and move it to desktop. Import malicous DLL to desktop and rename it to a valid DLL name that calc uses (WININET.dll)
   
   <img width="281" height="124" alt="image" src="https://github.com/user-attachments/assets/beb3b7f8-3906-40cd-86c4-06cc804acbe5" />

3. Install sysmon and configure event ID 7 (module load events) in the XML configuration file.

4. Monitor event ID 7 for calc exe to find suspicous behavior. An applications DLL should never run from a user writable folder like desktop in the picture below. Their is also no signature
       signifiying invalid DLL
   <img width="1082" height="334" alt="image" src="https://github.com/user-attachments/assets/91cb85f6-41e6-4c19-a8f3-65246521ed0c" />
---
# PowerShell/C-Sharp Injection
Attackers can inject C#/.NET code into a ordinary Windows process, converting it into a managed process. Attackers may do this to hide inside a process, run malicous code without dropping .exe, avoid antivirus detection, access Windows APIs, dump credentials, run recon, maintain persistence.
    - **Managed Process** is a process that is controlled by .NET CLR (Common Language Runtime) like            C#, Powershell, .NET code

  **Exploit**
  
    1. Gain access to user device
    
    2. Load C#/.NET payload loaded in memory using powershell
    
    3. Select target process to hide the payload

    4. Execute malicous code using process

 **Detection**

    1. Monitor for suspicous Powershell executions that suggest C# compiling or loading

    2. Monitor for native Windows process becoming managed

**Mitigations**

    1. Restrict PowerShell abuse

    2. Monitor and restrict process injection behavior

## Powershell Injection Lab

1. Inject an unmanaged PowerShell-like DLL into spoolsv.exe

    <img width="737" height="124" alt="image" src="https://github.com/user-attachments/assets/98f0444d-f3a9-423b-bd34-8fa6b289d338" />

2. Using **Process Hacker** monitor the state change for the spoolsv.exe process, specifically its change from unmanaged to managed

3. Using Sysmon, monitor Windows event ID 7. Determine if process loads DLLs like clr.dll and clrjit.dll, which signifys C# code is ran as part of the runtime execution. 

<img width="1031" height="499" alt="image" src="https://github.com/user-attachments/assets/e0d2cbfa-863d-4a5a-954c-556ef56f1e41" />

---
# Credential Dumping
Attacker tries to extract usernames, password hashes, plaintext passwords, kerberos tickets, or tokens. Attackers often target locations as such: LSASS memory, SAM database, Credential Manager, Powershell history, config files and scripts
    - Commonly used tool is mimikatz
    - LSASS (Local Security Authority Subsystem Service): Responsible for managing user credentials

 **Exploit**
  
    1. Gain access to user device
    
    2. Gain admin-level privileges
    
    3. Identify credential sources Ex. LSASS

    4. Extract credentials using tools

**Detection**

    1. Detect suspicous access to credential sources

    2. Monitor for file dumping credentials

    3. Monitor for suspicous process creation

Mitigations:

    1. Enable hardening for credential sources

    2. Enforce least privilege 

    3. If detection of dumping, rotate credentials immediately and quarantine device until its cleaned

## Credential Dumping Lab

1. Install and executre Mimikats tool to perform credential dumping

2. Monitor for Windows Event ID 10, which signifys that a process opened or accessed another process

<img width="1019" height="388" alt="image" src="https://github.com/user-attachments/assets/86e11e83-0250-4676-832f-6e9162072232" />
        AgentEXE.exe in user repository attempting to access lsass.exe process is suspicous

