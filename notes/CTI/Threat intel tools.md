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