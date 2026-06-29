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



## Lessons Learned
