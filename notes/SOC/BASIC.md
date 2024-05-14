has tools - Various online tools can be used to do hash lookups like [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).

mailicious ip blocking - One of the ways an adversary can make it challenging to successfully carry out IP blocking is by using Fast Flux.

domain names 
ttackers usually hide the malicious domains under **URL Shorteners.** A URL Shortener is a tool that creates a short and unique URL that will redirect to the specific website specified during the initial step of setting up the URL Shortener link. According to [Cofense](https://cofense.com/url-shorteners-fraudsters-friend/), attackers use the following URL Shortening services to generate malicious links: 
- bit.ly
- goo.gl
- ow.ly
- s.id
- smarturl.it
- tiny.pl
- tinyurl.com
- x.co

A network artifact can be a user-agent string, C2 information, or URI patterns followed by the HTTP POST requests.An attacker might use a User-Agent string that hasn’t been observed in your environment before or seems out of the ordinary. The User-Agent is defined by [RFC2616](https://datatracker.ietf.org/doc/html/rfc2616#page-145) as the request-header field that contains the information about the user agent originating the request.
- Network artifacts can be detected in Wireshark PCAPs (file that contains the packet data of a network) by using a network protocol analyzer such as [TShark](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) or exploring IDS (Intrusion Detection System) logging from a source such as [Snort](https://www.snort.org/).

Attackers would use the utilities to create malicious macro documents (maldocs) for spearphishing attempts, a backdoor that can be used to establish C2 (Command and Control Infrastructure), any custom .EXE, and .DLL files, payloads, or password crackers.
[MalwareBazaar](https://bazaar.abuse.ch/) and [Malshare](https://malshare.com/) are good resources to provide you with access to the samples, malicious feeds, and YARA results - these all can be very helpful when it comes to threat hunting and incident response. 

For detection rules, [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) is a great platform, where security professionals share their detection rules for different kinds of threats including the latest CVE's that are being exploited in the wild by adversaries.

fuzzy hasing - https://ssdeep-project.github.io/ssdeep/index.html

TTPs stands for Tactics, Techniques & Procedures. This includes the whole [MITRE](https://attack.mitre.org/) [ATT&CK Matrix](https://attack.mitre.org/), which means all the steps taken by an adversary to achieve his goal, starting from phishing attempts to persistence and data exfiltration.


## cyber kill chain
### reconissance
- [theHarvester](https://github.com/laramies/theHarvester) - other than gathering emails, this tool is also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources 
- [Hunter.io](https://hunter.io/) - this is  an email hunting tool that will let you obtain contact information associated with the domain
- [OSINT Framework](https://osintframework.com/) - OSINT Framework provides the collection of OSINT tools based on various categories
### weaponization
**Malware** is a program or software that is designed to damage, disrupt, or gain unauthorized access to a computer.

An **exploit** is a program or a code that takes advantage of the vulnerability or flaw in the application or system.

A **payload** is a malicious code that the attacker runs on the system.
reference - https://www.trustedsec.com/blog/intro-to-macros-and-vba-for-script-kiddies/
https://attack.mitre.org/tactics/TA0011/

### delivery 
https://www.csoonline.com/article/3534693/cybercriminal-group-mails-malicious-usb-dongles-to-targeted-companies.html
can be done in many ways

### exploiting
- The victim triggers the exploit by opening the email attachment or clicking on a malicious link.
- Using a zero-day exploit.
- Exploit software, hardware, or even human vulnerabilities. 
- An attacker triggers the exploit for server-based vulnerabilities.
are examples of exploiting 

### installing
https://attack.mitre.org/techniques/T1547/001/
refer to above website installing a webshell requires stable bacdoor


### command and control (C&C or C2)
- The protocols HTTP on port 80 and HTTPS on port 443 - this type of beaconing blends the malicious traffic with the legitimate traffic and can help the attacker evade firewalls.    
    
- DNS (Domain Name Server). The infected machine makes constant DNS requests to the DNS server that belongs to an attacker, this type of C2 communication is also known as DNS Tunneling.

## Threat modeling
- Identifying what systems and applications need to be secured and what function they serve in the environment. For example, is the system critical to normal operations, and is a system holding sensitive information like payment info or addresses?
- Assessing what vulnerabilities and weaknesses these systems and applications may have and how they could be potentially exploited
- Creating a plan of action to secure these systems and applications from the vulnerabilities highlighted
- Putting in policies to prevent these vulnerabilities from occurring again where possible (for example, implementing a software development life cycle (SDLC) for an application or training employees on phishing awareness).


## Uified Kill Chain
![[Pasted image 20240513184849.png]]

below are the phases
![[Pasted image 20240513184910.png]]

**Refer**
https://attack.mitre.org/tactics

![[Pasted image 20240513185319.png]]
After all the hunting for access and assets, the adversary will be seeking to gather all the valuable data of interest. This, in turn, compromises the confidentiality of the data and would lead to the next attack stage – Exfiltration. The main target sources include drives, browsers, audio, video and email.

### Diamond Model
The Diamond Model can help you identify the elements of an intrusion. At the end of this room, you will create a Diamond Model for events such as a breach, intrusion, attack, or incident. You will also be able to analyze an Advanced Persistent Threat (APT).
- Adversory
- Victim
- Capability
- Infrastructure
- Event meta features
- Social-poltical component
- Tech component
reference - https://www.activeresponse.org/wp-content/uploads/2013/07/diamond.pdf

### TTP
- The Tactic is the adversary's goal or objective.
- The Technique is how the adversary achieves the goal or objective.
- The Procedure is how the technique is executed.

APT's - https://www.mandiant.com/resources/insights/apt-groups

ATT&CK matrix
![[Pasted image 20240513190106.png]]

refer - https://attack.mitre.org/

https://mitre-attack.github.io/attack-navigator//#layerURL=https%3A%2F%2Fattack.mitre.org%2Fgroups%2FG0008%2FG0008-enterprise-layer.json

above link is TT&CK® Navigator for Carbanak.
![[Pasted image 20240513190328.png]]

we can use the ATT&CK Matrix to map a threat group to their tactics and techniques

cyber analystics Repository - https://car.mitre.org/
"_MITRE Engage is a framework for planning and discussing adversary engagement operations that empowers you to engage your adversaries and achieve your cybersecurity goals._"
https://engage.mitre.org/
https://engage.mitre.org/starter-kit/
 Engage website provides a [starter kit](https://engage.mitre.org/starter-kit/) to get you 'started' with the Adversary Engagement Approach. The starter kit is a collection of whitepapers and PDFs explaining various checklists, methodologies, and processes to get you started.


https://d3fend.mitre.org/
D3FEND stands for Detection, Denial, and Disruption Framework Empowering Network Defense. 

At the time of this writing, there are 408 artifacts in the D3FEND matrix.
![[Pasted image 20240513190818.png]]

CTID

MITRE formed an organization named The [Center of Threat-Informed Defense](https://mitre-engenuity.org/cybersecurity/center-for-threat-informed-defense/) (CTID). This organization consists of various companies and vendors from around the globe.

Some of the companies and vendors who are participants of CTID:

- AttackIQ (founder)
- Verizon
- Microsoft (founder)
- Red Canary (founder)
- Splunk
Adversary Emulation Library & ATT&CK® Emulations Plans

The [Adversary Emulation Library](https://medium.com/mitre-engenuity/introducing-the-all-new-adversary-emulation-plan-library-234b1d543f6b) is a public library making adversary emulation plans a free resource for blue/red teamers. The library and the emulations are a contribution from CTID. There are several [ATT&CK® Emulation Plans](https://github.com/center-for-threat-informed-defense/adversary_emulation_library) currently available: [APT3](https://attack.mitre.org/resources/adversary-emulation-plans/), [APT29](https://github.com/center-for-threat-informed-defense/adversary_emulation_library/tree/master/apt29), and [FIN6](https://github.com/center-for-threat-informed-defense/adversary_emulation_library/tree/master/fin6). The emulation plans are a step-by-step guide on how to mimic the specific threat group. If any of the C-Suite were to ask, "how would we fare if APT29 hits us?" This can easily be answered by referring to the results of the execution of the emulation plan.

### Cyber threat intelligence

Classifications:
**Strategic Intel:** - high level intel

