In windows the process is tun by DLL and winAPI and it doesn't check for if the DLL is genuine DLL or not

Win API book by windows developers

most attacks on windows are happening with DLL injection

- if u can hack the application to load a malicious dll it's done you can access the system 
- so windows came with new policy that All DLL should be digitally signed and if the system verify that if the system verifies that if the DLL is signed by Microsoft or not and the process becomes slow so it doesn't check fo DLL if it's verified or not

Microsoft explorer is the most exploited browser and then it implemented security checks for everything so it became slow

virtualallow() - will allot bytes of memory 
the goal of attacker is to inject a malware via DLL 

#### 2 ways of attacking DLLs
DLL side loading attack
Reflective DLL injection

to exploit a process you need a vulnerability 
most vulnerability is buffer overflow in process

if the process is overloaded with more data or function it will splill out the lower function

the antivirus works only if the files stores in the disk not in memory 
if you want to call a DLl function via disk then antivirus comes into play and stops it to evade this reflective DLl injection is created

DLL are 2 types - 1 types are system32 DLL used by windows system process
-2 2nd set of DLL comes with programs (stored in the same folder where the DLL is running)

- address spaces
- Raw DLL

meterpreter in Metasploit  is a payload works on deflective DLL injection 
- find vuln
- build payload
- push payload
- exploit system

### networking tool
Wireshark uses a library called tcp dump used to sniff packets
`tcpdump -ni any
every connection is based on 4 things
source ip source port dest ip dest port
#### Metasploit 
modules in
Auxiliary- network scanning (vulnerability assessment)
exploit -using this you can take the control of the system
once machine is exploited you need to put payload in that machine
3 types of payload 
- single (stand-alone)
- staged (go there and get executed (connect back to attacker machine))
- stager (the more payloads send to the the stage payload is stager payload) (bigger payload than stager)
payload - malicious code -(we encode it)
encoder module is used for this (obfuscation)
Nops adds lot's of 0's to payload for buffer overflow

![[Pasted image 20240619124114.png]]

![[Pasted image 20240619124237.png]]

the above is the list of smb payloads
to access the the metaplsoit framework we need a console
- msfconsole is popularly used

ps aux is used to get pID


web shell atatcks and server side attacks 