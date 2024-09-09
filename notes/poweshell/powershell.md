
powerful CLI interpreter and task oriented scripting language env on most win OS

- used by sys admin for managing win sys and automating tasks 
- integrated on .net framework 

![[Pasted image 20240909200039.png]]

 github.com/powershell/poershell

Cmdlet Overview:
https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7.4

Command-line Interpreter:
https://en.wikipedia.org/wiki/Command-line_interface#Command-Iine_interpreter

Component Obiect Model (COMI:
https://en.wikipedia.org/wiki/Component—Object_Model
https://learn.microsoft.com/en-us/windows/win32/com/component-object-model--com--portal

Investigating PowerShell: Command and Script loqqinq:
https://www.crowdstrike.com/blog/investigating-powershell-command-and-script-logging/

Windows Management Instrumentation (WMI):
https://en.wikipedia.org/wiki/Windows_Management_lnstrumentation

https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page

Why?
- takes advantage of living off the land concept where using tools that are built into OS work to our advantage once we've obtained access to system
- better control over the shell or system that u've been compromised
- Many organizations aren't actively hunting for PowerShell activity since it is usually considered a "trusted" application.
- We can use PowerShell to run, download or execute code, entirely within the memory process of the PowerShell executable, helping us evade endpoint security solutions.
- We can use it to interface with the .NET and other Windows APIs.



