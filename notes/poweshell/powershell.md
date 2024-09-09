
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
ex : API hooking and all
- We can call Windows DLL functions from within PowerShell.
- We can use it to bypass application whitelisting implementations by running the usual operating system commands from the PowerShell CLI.
- Many tools are already available to us for a large number of purposes related to penetration testing.
- Having access to all of those things through PowerShell helps us reduce our footprint and evade defense mechanisms while conducting post-exploitation tasks. 
- PowerShell is also easy to use, and there are many scripts and frameworks written that we can utilize for our offensive purposes.
- Furthermore, it doesn't take much to create our own scripts to carry out some of our tasks as we'll see in the modules that follow.

 Living Off the Land:
https://www.secureworks.com/blog/living-off-the-land

PowerShell: 
https://en.wikipedia.org/wiki/PowerSheII

PowerSploit:
https://github.com/PowerShellMafia/PowerSploit

The PowerShell CLI provides us with access to built-in cmdlets, modules, functions, features, and provides way to create tasks, functions, variables interactively, and more, directly from the CLI.

![[Pasted image 20240909204456.png]]

![[Pasted image 20240909204533.png]]

![[Pasted image 20240909204602.png]]

![[Pasted image 20240909204730.png]]

![[Pasted image 20240909204821.png]]

![[Pasted image 20240909204857.png]]

![[Pasted image 20240909204947.png]]

![[Pasted image 20240909204957.png]]

![[Pasted image 20240909205004.png]]

### Version:

- We can use the -Version parameter followed by a version number as the argument to downgrade the version of PowerShell. 
- Useful in scenarios where you've landed on a machine with a more recent version and need to downgrade to Version 1.0 or 2.0 or to complete certain tasks.
- Requires that older versions are still installed on the target.
		`C: \ > power shell .exe -Version 2`

![[Pasted image 20240909205145.png]]

![[Pasted image 20240909205228.png]]

![[Pasted image 20240909205312.png]]

More information on using the "Get-Help" cmdlet can
be found here:
https://learn.microsoft.com/en-us/previous-versions/system-center/virtual-machine-manager-2008-r2/cc764318(v=technet.10)?redirectedfrom=MSDN

![[Pasted image 20240909205404.png]]

