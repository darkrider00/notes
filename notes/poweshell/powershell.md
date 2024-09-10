
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

### running the basic commands

- to check if we r running 64 bit or 32 bit powershell the command is 
		`[environment]::Is64BitProcess`

![[Pasted image 20240909205937.png]]

above is powershell with admin privileges

![[Pasted image 20240909210003.png]]


we can use tab to autocomplete for commands in powershell

above is PowerShell (X86)

- setting execution policy to unrestircted 

![[Pasted image 20240909210554.png]]


![[Pasted image 20240909210640.png]]


- script to open calclulator 

![[Pasted image 20240909211627.png]]

as soon as i executed the command without opening PowerShell windows calculator opened 

instead or -ExecutionPolicy we can use -ep

- command to get all windows security logs
![[Pasted image 20240909212231.png]]

command : `powershell.exe -ep Unrestricted -Command "& { GET-EventLog -LogName security`


### cmdlets

- cmdlets are light weight PowerShell scripts that perform a single function 
- most cmdlets by default will return a limited set of information or columns
- command : `Get-Children | Format-list *`
- names whether in list format or default column format are important , as we can use those to filter the output  of cmdlet objects for specific properties
- usually cmdlets outputs are referred to objects
- objects can be further processed using what is known as pipelining (similar to how we can chain commands together)
- example : `Get-Process | Sort-Object -Unique| select-Object ProcessName`

![[Pasted image 20240910180348.png]]

- as we can see if we jsut type Get-Process command we get more colums 
- we can sort it by the process name using the above command
![[Pasted image 20240910180604.png]]

as we can see we get only process id names , apart from process name we can specify other parameters that we want to display then the command would be 

`Get-Process | Sort-Object -Unique |Select-Object ProcessName , Handles`

![[Pasted image 20240910181000.png]]

- we can redirect the results of our pipeline to a file using a standard operator the command would be 
`Get-Process | Sort-Object -Unique |Select-Object ProcessName > unique_process.txt`
let's execute it 

![[Pasted image 20240910181345.png]]

