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

  **How ETW can help detect .NET assembly loading:**
  EX.

  <img width="947" height="86" alt="image" src="https://github.com/user-attachments/assets/030b2e42-b702-437f-84c6-47bd8c520f45" />

  This command allows defender to view 0x2083 events which allows monitoring of .NET events. These events include subsets such as JitKeyword, InteropKeyword, LoaderKeyword, NGenKeyword.

    1) JitKeyword (Just-In-Time): compilation events, providing information on the methods being compiled at runtime.
    2) InteropKeyword: Events that include manged code interacting with unmanaged code.
    3) LeaderKeyword:  Provides details on the assembly loading process within the .NET runtime
    4) NGenKeyword:  Native Image Generator which includes the creation and usage of precompiled .NET assemblies.
  

          


  


