# Detecting Using ETW

## Key Concepts
- **Event Tracing for Windows** is a built in Windows tracing system that lets Windows and applications generate detailed telemetry about what is happening on the system.

---
## Detecting Strange Child-Parent Relationships
**Parent-Child Relationships** are processes that initiate another process. Deviations from normal Parent-Child relationships can indicate compromise

## Parent-Child Spoofing
  Parent-Child relationships can be spoofed to give off the perception a native Windows process initiated   process instead of a potential alarming process like powershell.

  Ex. 
  <img width="854" height="139" alt="image" src="https://github.com/user-attachments/assets/bc8f5c75-5783-4088-a328-dad1f16aa0a5" />
      This image demonstrates how a parent process can be spoofed. In this specific example, this will          display a windows event showing that spoolsv.exe initiated the cmd.exe and not powershell

  Using SilkETW we can more accurately acquire logs that truthfully represent the process initiation.       Using SilkETW we can now see that powershell actually initiated cmd.exe and not spoolsv.exe
  <img width="949" height="64" alt="image" src="https://github.com/user-attachments/assets/f5b5e298-b5fb-4584-ae5e-c985708f771a" />

---
## Detecting Malicious .NET Assembly Loading
  - **Living of the land**: Using tools that are already native to the environment
  - **Bring your own land**: Bring custom tools and run directly in memory instead of saving it as an           obvious .exe or .dll on disk. This leaves fewer IOCs for defenders to detect.
    
encoded/encrypted payload → loaded into memory → CLR loads the assembly → code runs without a normal executable being dropped to disk

  

