Threat intel is understanding the relationship b/w your operational environment and adversary

### Strategic Intelligence

**Purpose:** To provide a high-level overview of the threat landscape that an organization faces.

- **Focus:** Long-term trends, patterns, and emerging threats.
- **Audience:** Senior management and decision-makers.
- **Usage:** Helps in strategic planning and making informed business decisions.
- **Example:** Analyzing geopolitical tensions that could lead to increased cyber attacks on financial institutions over the next year.

**Key Points:**

- Informs risk management and business strategies.
- Maps out potential future threats and their impact on the organization.
- Helps in allocating resources and setting priorities for security investments.

### Technical Intelligence

**Purpose:** To provide detailed information on the technical aspects of attacks.

- **Focus:** Evidence and artifacts from cyber attacks.
- **Audience:** Incident response teams and technical security personnel.
- **Usage:** Helps in understanding and mitigating specific threats by analyzing attack methods and tools.
- **Example:** Analyzing a malware sample to understand how it operates and spreads.

**Key Points:**

- Identifies the tools and techniques used by attackers.
- Provides insights for developing defense mechanisms.
- Helps in creating a baseline of the attack surface for monitoring and detection.

### Tactical Intelligence

**Purpose:** To understand the specific tactics, techniques, and procedures (TTPs) used by adversaries.

- **Focus:** Real-time investigations and immediate threat responses.
- **Audience:** Security operations teams and analysts.
- **Usage:** Helps in strengthening security controls and addressing vulnerabilities.
- **Example:** Identifying and responding to a phishing campaign targeting employees with specific lures.

**Key Points:**

- Assesses the methods used by attackers to breach systems.
- Provides actionable insights for improving defensive measures.
- Helps in real-time threat hunting and incident response.

### Operational Intelligence

**Purpose:** To understand the specific motives and intent behind an adversary's actions.

- **Focus:** The adversary’s goals, strategies, and specific attack plans.
- **Audience:** Security teams and threat analysts.
- **Usage:** Helps in protecting critical assets by understanding what might be targeted.
- **Example:** Investigating a specific threat actor’s plans to disrupt an organization's supply chain.

**Key Points:**

- Looks at the why behind an attack—motives and objectives.
- Identifies the most likely targets within the organization.
- Helps in developing targeted defensive strategies to protect critical assets (people, processes, and technologies).

### Summary

- **Strategic Intelligence:** Big-picture view, guiding long-term planning.
- **Technical Intelligence:** Detailed technical analysis of attack methods.
- **Tactical Intelligence:** Real-time response and immediate threat management.
- **Operational Intelligence:** Understanding adversary motives to protect critical assets.

Each type of threat intelligence serves a unique purpose and caters to different audiences within an organization, all aimed at enhancing the overall security posture.


urlscan.,io is a free service developed to assist in scanning and analysing website 
- used to automate the process of browsing and crawling through website to record activities and interactions 

![[db3fb7276dd4c303a5ef7aa04a2ad8a0.gif]]

### How URLscan.io Works

1. **Submission of URL:**
    
    - Users submit a URL through the URLscan.io website interface, API, or browser extension.
    - The URL can be any web address that the user wants to analyze for security purposes or to understand its behavior.
2. **Webpage Rendering:**
    
    - URLscan.io uses a headless browser (a browser without a graphical user interface) to load the submitted URL.
    - The headless browser simulates a real user visiting the webpage, allowing URLscan.io to capture and analyze the behavior of the site.
3. **Data Collection:**
    
    - As the webpage loads, URLscan.io collects various data points, including:
        - **HTTP Requests and Responses:** Details of all network requests made by the webpage, including resources like images, scripts, and stylesheets.
        - **DOM Analysis:** The Document Object Model (DOM) structure of the webpage, which represents the HTML content and elements.
        - **JavaScript Execution:** Analysis of any JavaScript code executed by the webpage.
        - **Cookies and Storage:** Information about cookies set by the webpage and other storage mechanisms like LocalStorage and SessionStorage.
4. **Security Analysis:**
    
    - URLscan.io performs various security checks to identify potential threats, such as:
        - **Phishing Detection:** Analyzing content and behavior to detect phishing attempts.
        - **Malware Detection:** Identifying malicious scripts or resources that may be harmful to users.
        - **Blacklist Checks:** Comparing the URL against known blacklists to see if it has been reported for malicious activity.
5. **Visualization and Reporting:**
    
    - The results of the scan are presented in a detailed report that includes:
        - **Screenshot:** A visual representation of how the webpage looks when loaded.
        - **HTTP Request Map:** A visualization of all network requests made by the webpage, showing the domains contacted and resources loaded.
        - **Resource List:** A comprehensive list of all resources loaded by the webpage, including their types, URLs, and sizes.
        - **Security Findings:** Any security issues identified during the scan, such as suspicious content or behavior.
6. **Integration and Automation:**
    
    - URLscan.io provides an API that allows users to automate URL submissions and retrieve scan results programmatically.
    - Users can integrate URLscan.io with other security tools and workflows to enhance their threat detection and analysis capabilities.

### Use Cases

1. **Threat Intelligence:**
    
    - Security analysts use URLscan.io to investigate suspicious URLs and gather intelligence on potential threats.
    - It helps in identifying phishing sites, malware distribution points, and other malicious activities.
2. **Incident Response:**
    
    - During security incidents, URLscan.io can be used to analyze URLs related to the incident, providing insights into the scope and nature of the threat.
    - Helps in understanding how a compromised site behaves and what resources it loads.
3. **Malware Analysis:**
    
    - Researchers use URLscan.io to study how malware is distributed through compromised websites.
    - Analyzes the network activity and resources loaded by malware-infected sites.
4. **Phishing Detection:**
    
    - Organizations use URLscan.io to detect and block phishing sites targeting their employees or customers.
    - Provides detailed reports that help in taking down phishing sites.

## Scan Results

URL scan results provide ample information, with the following key areas being essential to look at:

- **Summary:** Provides general information about the URL, ranging from the identified IP address, domain registration details, page history and a screenshot of the site.
- **HTTP:** Provides information on the HTTP connections made by the scanner to the site, with details about the data fetched and the file types received.
- **Redirects:** Shows information on any identified HTTP and client-side redirects on the site.
- **Links:** Shows all the identified links outgoing from the site's homepage.
- **Behaviour:** Provides details of the variables and cookies found on the site. These may be useful in identifying the frameworks used in developing the site.
- **Indicators:** Lists all IPs, domains and hashes associated with the site. These indicators do not imply malicious activity related to the site.!

![[5ba68bbdd6e7e9ef2bbe2a0dc13106bc 1.gif]]

abuse.ch is dedicated to gathering and disseminating information about cyber threats to assist organizations in protecting their networks and systems. The organization collaborates with security researchers, law enforcement agencies, and industry partners to provide timely and accurate threat intelligence.

### Main Projects

1. **URLhaus:**
    
    - **Purpose:** To collect and share information about malicious URLs that distribute malware.
    - **How It Works:** Security researchers and organizations can submit URLs to URLhaus. The platform verifies and catalogs these URLs, providing data on the type of malware being distributed, the hosting infrastructure, and other relevant details.
    - **Usage:** Users can search the URLhaus database for specific URLs or download feeds of malicious URLs to integrate into their security systems for blocking and monitoring purposes.
2. **ThreatFox:**
    
    - **Purpose:** To provide a platform for sharing indicators of compromise (IOCs) related to malware.
    - **How It Works:** Users can submit IOCs such as IP addresses, domain names, file hashes, and URLs associated with malware. ThreatFox aggregates this data and makes it available to the security community.
    - **Usage:** Security teams can use ThreatFox to enhance their threat detection and response capabilities by incorporating the shared IOCs into their security tools.
3. **Feodo Tracker:**
    
    - **Purpose:** To track and mitigate Feodo (also known as Cridex or Bugat) botnet activity.
    - **How It Works:** Feodo Tracker monitors command and control (C&C) servers used by the Feodo botnet. It provides a list of active C&C servers, including their IP addresses, domains, and associated malware families.
    - **Usage:** Organizations can use the information from Feodo Tracker to block communication with these C&C servers and prevent botnet infections.
4. **MalwareBazaar:**
    
    - **Purpose:** To facilitate the sharing of malware samples among the security community.
    - **How It Works:** Users can upload malware samples to MalwareBazaar. The platform analyzes and catalogs these samples, providing metadata such as file hashes, malware family, and associated IOCs.
    - **Usage:** Researchers and analysts can download samples for analysis, enhancing their understanding of malware behavior and improving detection techniques.

### How abuse.ch Works

1. **Data Collection:**
    
    - abuse.ch relies on contributions from security researchers, organizations, and automated systems to collect data on malicious activities. This includes submissions of URLs, IP addresses, domain names, and malware samples.
2. **Verification and Analysis:**
    
    - Submitted data undergoes verification and analysis to ensure its accuracy and relevance. For example, URLs submitted to URLhaus are checked to confirm they are actively distributing malware.
3. **Database Management:**
    
    - Verified data is stored in databases and made accessible to the security community. abuse.ch maintains various databases for different types of threats, such as malicious URLs, botnet C&C servers, and malware samples.
4. **Information Sharing:**
    
    - abuse.ch provides multiple ways for users to access and utilize the collected data. This includes searchable databases, downloadable feeds, APIs, and integration with other security tools.

It was developed to identify and track malware and botnets through several operational platforms developed under the project. These platforms are:

- **Malware Bazaar:**  A resource for sharing malware samples.
- **Feodo Tracker:**  A resource used to track botnet command and control (C2) infrastructure linked with Emotet, Dridex and TrickBot.
- **SSL Blacklist:**  A resource for collecting and providing a blocklist for malicious SSL certificates and JA3/JA3s fingerprints.
- **URL Haus:**  A resource for sharing malware distribution sites.
- **Threat Fox:**  A resource for sharing indicators of compromise (IOCs).
- 
### Use Cases

1. **Threat Intelligence:**
    
    - Organizations use abuse.ch’s data to enhance their threat intelligence capabilities. By incorporating information about malicious URLs, IOCs, and malware samples, they can improve their detection and prevention measures.
2. **Incident Response:**
    
    - During security incidents, incident response teams can leverage abuse.ch’s data to identify and mitigate threats. For example, they can use URLhaus to find malicious URLs involved in a phishing campaign.
3. **Research and Analysis:**
    
    - Security researchers use abuse.ch’s resources to study malware behavior, track botnet activities, and develop new detection techniques. MalwareBazaar, in particular, is valuable for accessing a wide range of malware samples.
4. **Network Protection:**
    
    - Network administrators and security teams use data from abuse.ch to block malicious traffic and prevent infections. For instance, they can use Feodo Tracker to block communication with botnet C&C servers.
## [MalwareBazaar](https://bazaar.abuse.ch/)

As the name suggests, this project is an all in one malware collection and analysis database. The project supports the following features:

- **Malware Samples Upload:** Security analysts can upload their malware samples for analysis and build the intelligence database. This can be done through the browser or an API.
- **Malware Hunting:** Hunting for malware samples is possible through setting up alerts to match various elements such as tags, signatures, YARA rules, ClamAV signatures and vendor detection.

![[55890b3448b3ecf9a55705cd1bd20b08.gif]]

## [FeodoTracker](https://feodotracker.abuse.ch/)

With this project, Abuse.ch is targeting to share intelligence on botnet Command & Control (C&C) servers associated with Dridex, Emotes (aka Heodo), TrickBot, QakBot and BazarLoader/BazarBackdoor. This is achieved by providing a database of the C&C servers that security analysts can search through and investigate any suspicious IP addresses they have come across. Additionally, they provide various IP and IOC blocklists and mitigation information to be used to prevent botnet infections.

![[22e34a463f65fbf7e621a54e347543be.gif]]
## [SSL Blacklist](https://sslbl.abuse.ch/)

Abuse.ch developed this tool to identify and detect malicious SSL connections. From these connections, SSL certificates used by botnet C2 servers would be identified and updated on a denylist that is provided for use. The denylist is also used to identify JA3 fingerprints that would help detect and block malware botnet C2 communications on the TCP layer.

You can browse through the SSL certificates and JA3 fingerprints lists or download them to add to your deny list or threat hunting rulesets.

![[78bb7ba13a89c203b3ed331df18e2c4d.gif]]

## [URLhaus](https://urlhaus.abuse.ch/)

As the name points out, this tool focuses on sharing malicious URLs used for malware distribution. As an analyst, you can search through the database for domains, URLs, hashes and filetypes that are suspected to be malicious and validate your investigations.

The tool also provides feeds associated with country, AS number and Top Level Domain that an analyst can generate based on specific search needs.

![[f388122492011e9506410912afd749d1 1.gif]]
## [ThreatFox](https://threatfox.abuse.ch/)

With ThreatFox,  security analysts can search for, share and export indicators of compromise associated with malware. IOCs can be exported in various formats such as MISP events, Suricata IDS Ruleset, Domain Host files, DNS Response Policy Zone, JSON files and CSV files.

![[e0fffff3133f4641f85190228990bdfb 1.gif]]

IT and Cybersecurity companies collect massive amounts of information that could be used for threat analysis and intelligence. Being one of those companies, Cisco assembled a large team of security practitioners called Cisco Talos to provide actionable intelligence, visibility on indicators, and protection against emerging threats through data collected from their products. The solution is accessible as [Talos Intelligence](https://talosintelligence.com/).

Cisco Talos encompasses six key teams:

- **Threat Intelligence & Interdiction:** Quick correlation and tracking of threats provide a means to turn simple IOCs into context-rich intel.
- **Detection Research:** Vulnerability and malware analysis is performed to create rules and content for threat detection.
- **Engineering & Development:** Provides the maintenance support for the inspection engines and keeps them up-to-date to identify and triage emerging threats.
- **Vulnerability Research & Discovery:** Working with service and software vendors to develop repeatable means of identifying and reporting security vulnerabilities.
- **Communities:** Maintains the image of the team and the open-source solutions.
- **Global Outreach:** Disseminates intelligence to customers and the security community through publications.

More information about Cisco Talos can be found on their [White Paper](https://www.talosintelligence.com/docs/Talos_WhitePaper.pdf)

## Talos Dashboard

Accessing the open-source solution, we are first presented with a reputation lookup dashboard with a world map. This map shows an overview of email traffic with indicators of whether the emails are legitimate, spam or malware across numerous countries. Clicking on any marker, we see more information associated with IP and hostname addresses, volume on the day and the type.

![Talos Dashboard](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/e8ad635a9e449c698e081895bbb13ab1.png)  

At the top, we have several tabs that provide different types of intelligence resources. The primary tabs that an analyst would interact with are:  

- **Vulnerability Information:** Disclosed and zero-day vulnerability reports marked with CVE numbers and CVSS scores. Details of the vulnerabilities reported are provided when you select a specific report, including the timeline taken to get the report published. Microsoft vulnerability advisories are also provided, with the applicable snort rules that can be used.

![Talos Vulnerability Information Navigation](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/c761ada971950f5c2b676263d6e328a8.gif)

- **Reputation Center:** Provides access to searchable threat data related to IPs and files using their SHA256 hashes. Analysts would rely on these options to conduct their investigations. Additional email and spam data can be found under the **Email & Spam Data tab**.

![Talos Reputation Center](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/e14c377b524b9eb51b0a8ed8f1ee8356.gif)

  

![Talos Reputation Center](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/844f12e63a5a255b85df2ad6d261facb.gif)