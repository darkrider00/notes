- defined as evidence based knowledge about adversaries

data :  Discrete indicators associated with an adversary, such as IP addresses, URLs or hashes.

**Information:** A combination of multiple data points that answer questions such as “How many times have employees accessed tryhackme.com within the month?”

**Intelligence:** The correlation of data and information to extract patterns of actions based on contextual analysis.


- Who’s attacking you?
- What are their motivations?
- What are their capabilities?
- What artefacts and indicators of compromise (IOCs) should you look out for?

##### Threat Intelligence Classifications

- **Strategic Intelligence**:
- 
    - **What it is**: A broad, big-picture look at potential risks and threats to the organization.
    
    - **Purpose**: Helps senior leaders understand long-term risks based on trends and patterns in the threat landscape.
    
    - **Example**: Noticing an increase in ransomware attacks globally and deciding to invest in better backup systems to mitigate future risks.

- **Technical Intelligence**:
    
    - **What it is**: Detailed information about the tools and methods attackers use.
    
    - **Purpose**: Helps technical teams (like IT or security teams) understand how attacks happen so they can defend against them.
    
    - **Example**: Discovering a new type of malware and analyzing how it works so you can create defenses to block it.

- **Tactical Intelligence**:
    
    - **What it is**: Information about the specific techniques and strategies attackers use.
    
    - **Purpose**: Helps improve security measures and respond to attacks quickly.
    
    - **Example**: Learning that attackers are using phishing emails with specific subject lines, and then setting up filters to catch those emails.

- **Operational Intelligence**:
    
    - **What it is**: Insight into the specific goals and plans of attackers.
    
    - **Purpose**: Helps security teams understand which parts of the organization are most at risk.
    
    - **Example**: Finding out that a hacker group is targeting your company’s customer database, so you focus on securing that data


![[Pasted image 20240805213939.png]]

 obtained from a data-churning process that transforms raw data into contextualised and action-oriented insights geared towards triaging security incidents. The transformational process follows a six-phase cycle:

1. **Direction**:
    - **Purpose**: Set clear objectives and goals for your threat intelligence program.
    - **Key Activities**:
        - Identify what needs protection (important data and processes).
        - Assess the impact if these assets are lost or disrupted.
        - Determine sources of data and intelligence for protection.
        - Identify tools and resources needed for defense.
    - **Outcome**: Clear questions and goals for investigating incidents

1. **Collection**:
    - **Purpose**: Gather the necessary data to meet the objectives.
    - **Key Activities**:
        - Use various sources (commercial, private, open-source) to collect data.
        - Automate data collection to handle large volumes efficiently.
    - **Outcome**: A comprehensive set of raw data for analysis.

1. **Processing**:
    - **Purpose**: Organize and format the collected data.
    - **Key Activities**:
        - Extract, sort, and organize data.
        - Correlate data with tags and present it in an understandable format.
        - Use tools like SIEMs (Security Information and Event Management) to parse data quickly.
    - **Outcome**: Usable and organized data ready for analysis.

1. **Analysis**:
    - **Purpose**: Derive actionable insights from the processed data.
    - **Key Activities**:
        - Investigate potential threats by uncovering indicators and attack patterns.
        - Define action plans to prevent attacks and protect the infrastructure.
        - Enhance security controls or justify the need for additional resources.
    - **Outcome**: Clear insights and recommendations for defending against threats.

1. **Dissemination**:
    - **Purpose**: Share the intelligence with relevant stakeholders in appropriate formats.
    - **Key Activities**:
        - Provide concise reports for executives covering trends, financial implications, and strategic recommendations.
        - Share detailed technical information with the security team about threats, indicators of compromise (IOCs), and action plans.
    - **Outcome**: Stakeholders are informed and can take appropriate actions based on the intelligence.

1. **Feedback**:
    - **Purpose**: Improve the threat intelligence process through regular feedback.
    - **Key Activities**:
        - Gather responses from stakeholders about the intelligence provided.
        - Use feedback to enhance the threat intelligence process and security controls.
        - Maintain regular communication between teams to keep the cycle effective.
    - **Outcome**: Continuous improvement of the threat intelligence program.

By following these six phases, organizations can turn raw data into meaningful, actionable insights that help protect against security threats.


#### Standards and frameworks

Standards and frameworks provide structures to rationalise the distribution and use of threat intel across industries. They also allow for common terminology, which helps in collaboration and communication. Here, we briefly look at some essential standards and frameworks commonly used.

### MITRE ATT&CK

The [ATT&CK framework](https://tryhackme.com/room/mitre) is a knowledge base of adversary behaviour, focusing on the indicators and tactics. Security analysts can use the information to be thorough while investigating and tracking adversarial behaviour.  

![Image of the MITRE ATT&CK Matrix.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/5d94b9da7f9ddc77bd46895bc1b936d8.png)

### TAXII

[The Trusted Automated eXchange of Indicator Information (TAXII)](https://oasis-open.github.io/cti-documentation/taxii/intro) defines protocols for securely exchanging threat intel to have near real-time detection, prevention and mitigation of threats. The protocol supports two sharing models:

- Collection: Threat intel is collected and hosted by a producer upon request by users using a request-response model.
- Channel: Threat intel is pushed to users from a central server through a publish-subscribe model.

### STIX

[Structured Threat Information Expression (STIX)](https://oasis-open.github.io/cti-documentation/stix/intro) is a language developed for the "specification, capture, characterisation and communication of standardised cyber threat information". It provides defined relationships between sets of threat info such as observables, indicators, adversary TTPs, attack campaigns, and more.  

### Cyber Kill Chain

Developed by Lockheed Martin, the Cyber Kill Chain breaks down adversary actions into steps. This breakdown helps analysts and defenders identify which stage-specific activities occurred when investigating an attack. The phases defined are shown in the image below.

![Image of the seven steps of the Cyber Kill Chain.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/ef67be43aaf8073a8309df3e160c7e36.png)  

|Technique|Purpose|Examples|
|---|---|---|
|Reconnaissance|Obtain information about the victim and the tactics used for the attack.|Harvesting emails, OSINT, and social media, network scans|
|Weaponisation|Malware is engineered based on the needs and intentions of the attack.|Exploit with a backdoor, malicious office document|
|Delivery|Covers how the malware would be delivered to the victim's system.|Email, weblinks, USB|
|Exploitation|Breach the victim's system vulnerabilities to execute code and create scheduled jobs to establish persistence.|EternalBlue, Zero-Logon, etc.|
|Installation|Install malware and other tools to gain access to the victim's system.|Password dumping, backdoors, remote access trojans|
|Command & Control|Remotely control the compromised system, deliver additional malware, move across valuable assets and elevate privileges.|Empire, Cobalt Strike, etc.|
|Actions on Objectives|Fulfil the intended goals for the attack: financial gain, corporate espionage, and data exfiltration.|Data encryption, ransomware, public defacement|

Over time, the kill chain has been expanded using other frameworks such as ATT&CK and formulated a new Unified Kill Chain.

### The Diamond Model

![An illustration of the diamond model of intrusion analysis.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/d31177261479b466ecbe964447ac4f84.svg)

The diamond model looks at intrusion analysis and tracking attack groups over time. It focuses on four key areas, each representing a different point on the diamond. These are:

- **Adversary:** The focus here is on the threat actor behind an attack and allows analysts to identify the motive behind the attack.
- **Victim:** The opposite end of adversary looks at an individual, group or organisation affected by an attack.
- **Infrastructure:** The adversaries' tools, systems, and software to conduct their attack are the main focus. Additionally, the victim's systems would be crucial to providing information about the compromise.
- **Capabilities:** The focus here is on the adversary's approach to reaching its goal. This looks at the means of exploitation and the TTPs implemented across the attack timeline

An example of the diamond model in play would involve an adversary targeting a victim using phishing attacks to obtain sensitive information and compromise their system, as displayed on the diagram. As a threat intelligence analyst, the model allows you to pivot along its properties to produce a complete picture of an attack and correlate indicators.


CTI is also distributed to organisations using published threat reports. These reports come from technology and security companies that research emerging and actively used threat vectors. They are valuable for consolidating information presented to all suitable stakeholders. Some notable threat reports come from [Mandiant](https://www.mandiant.com/resources), [Recorded Future](https://www.recordedfuture.com/resources/global-issues) and [AT&TCybersecurity](https://cybersecurity.att.com/).

All the things we have discussed come together when mapping out an adversary based on threat intel. To better understand this, we will analyse a simplified engagement example. Click on the green “**View Site**” button in this task to open the Static Site Lab and navigate through the security monitoring tool on the right panel and fill in the threat details.

