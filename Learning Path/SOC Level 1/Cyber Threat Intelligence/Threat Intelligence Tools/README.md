![image](https://user-images.githubusercontent.com/51442719/182532569-9f2dc531-87ef-4a96-b4d0-a4eb05822cf7.png)
# [Threat Intelligence Tools](https://tryhackme.com/room/threatinteltools)
![image](https://user-images.githubusercontent.com/51442719/182532556-26e4506f-7921-4b44-b42b-66d2bf21b8d7.png)
> ### Explore different OSINT tools used to conduct security threat assessments and investigations.

- [ ] [Task 1  Room Outline](#task-1--room-outline)
- [ ] [Task 2  Threat Intelligence](#task-2--threat-intelligence)
- [ ] [Task 3  UrlScan.io](#task-3--urlscanio)
- [ ] [Task 4  Abuse.ch](#task-4--abusech)
- [ ] [Task 5  PhishTool](#task-5--phishtool)
- [ ] [Task 6  Cisco Talos Intelligence](#task-6--cisco-talos-intelligence)
- [ ] [Task 7  Scenario 1](#task-7--scenario-1)
- [ ] [Task 8  Scenario 2](#task-8--scenario-2)
- [ ] [Task 9  Conclusion](#task-9--conclusion)

---

## [Task 1  Room Outline]()

#### This room will cover the concepts of Threat Intelligence and various open-source tools that are useful. 

### The learning objectives include:
- Understanding the basics of threat intelligence & its classifications.
- Using UrlScan.io to scan for malicious URLs.
- Using Abuse.ch to track malware and botnet indicators.
- Investigate phishing emails using PhishTool
- Using Cisco's Talos Intelligence platform for intel gathering.

---

## [Task 2  Threat Intelligence]()

#### Threat Intelligence is the analysis of data and information using tools and techniques to generate meaningful patterns on how to mitigate against potential risks associated with existing or emerging threats targeting organisations, industries, sectors or governments.

### To mitigate against risks, we can start by trying to answer a few simple questions:
- Who's attacking you?
- What's their motivation?
- What are their capabilities?
- What artefacts and indicators of compromise should you look out for?

### Threat Intelligence Classifications:
- Threat Intel is geared towards understanding the relationship between your operational environment and your adversary. 

### With this in mind, we can break down threat intel into the following classifications: 

- **Strategic Intel**: 
  - High-level intel that looks into the organisation's threat landscape and maps out the risk areas based on trends, patterns and emerging threats that may impact business decisions.

- **Technical Intel**: 
  - Looks into evidence and artefacts of attack used by an adversary. 
  - Incident Response teams can use this intel to create a baseline attack surface to analyse and develop defence mechanisms.

- **Tactical Intel**: 
  - Assesses adversaries' tactics, techniques, and procedures (TTPs). 
  - This intel can strengthen security controls and address vulnerabilities through real-time investigations.

- **Operational Intel**: 
  - Looks into an adversary's specific motives and intent to perform an attack. 
  - Security teams may use this intel to understand the critical assets available in the organisation (people, processes, and technologies) that may be targeted.


---

## [Task 3  UrlScan.io]()

#### [Urlscan.io](https://urlscan.io/) is a free service developed to assist in scanning and analysing websites. 
- It is used to automate the process of browsing and crawling through websites to record activities and interactions.

#### When a URL is submitted, the information recorded includes the domains and IP addresses contacted, resources requested from the domains, a snapshot of the web page, technologies utilised and other metadata about the website.
- The site provides two views, the first one showing the most recent scans performed and the second one showing current live scans.
![image](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/db3fb7276dd4c303a5ef7aa04a2ad8a0.gif)

![image](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/5ba68bbdd6e7e9ef2bbe2a0dc13106bc.gif)

### Scan Results
#### URL scan results provide ample information, with the following key areas being essential to look at:
- **Summary**: 
  - Provides general information about the URL, ranging from the identified IP address, domain registration details, page history and a screenshot of the site.
- **HTTP**: 
  - Provides information on the HTTP connections made by the scanner to the site, with details about the data fetched and the file types received.
- **Redirects**: 
  - Shows information on any identified HTTP and client-side redirects on the site.
- **Links**: 
  - Shows all the identified links outgoing from the site's homepage.
- **Behaviour**: 
  - Provides details of the variables and cookies found on the site. 
  - These may be useful in identifying the frameworks used in developing the site.
- **Indicators**: Lists all IPs, domains and hashes associated with the site. These indicators do not imply malicious activity related to the site.

### Scenario
- You have been tasked to perform a scan on TryHackMe's domain. 
- The results obtained are displayed in the image below. 

#### Use the details on the image to answer the questions:
![image](https://user-images.githubusercontent.com/51442719/182537390-49586d26-7421-43d0-a764-c2ef0832a581.png)

### Answer the questions below

- What is TryHackMe's Cisco Umbrella Rank?
  > Answer format: ******
- How many domains did UrlScan.io identify?
  > Answer format: **
- What is the main domain registrar listed?
  > Answer format: ********* ***
- What is the main IP address identified?
  > Answer format: ****:****:**::****:****


---

## [Task 4  Abuse.ch]()

[Abuse.ch](https://abuse.ch/) is a research project hosted by the Institue for Cybersecurity and Engineering at the Bern University of Applied Sciences in Switzerland.  
It was developed to identify and track malware and botnets through several operational platforms developed under the project.  

These platforms are**:
- **Malware Bazaar**:  A resource for sharing malware samples.
- **Feodo Tracker**:  A resource used to track botnet command and control (C2) infrastructure linked with Emotet, Dridex and TrickBot.
- **SSL Blacklist**:  A resource for collecting and providing a blocklist for malicious SSL certificates and JA3/JA3s fingerprints.
- **URL Haus**:  A resource for sharing malware distribution sites.
- **Threat Fox**:  A resource for sharing indicators of compromise (IOCs).

Let us look into these platforms individually.

### [MalwareBazaar](https://bazaar.abuse.ch/)
As the name suggests, this project is an all in one malware collection and analysis database. The project supports the following features:

- **Malware Samples Upload**: Security analysts can upload their malware samples for analysis and build the intelligence database. This can be done through the browser or an API.
- **Malware Hunting**: Hunting for malware samples is possible through setting up alerts to match various elements such as tags, signatures, YARA rules, ClamAV signatures and vendor detection.

### [FeodoTracker](https://feodotracker.abuse.ch/)
With this project, Abuse.ch is targeting to share intelligence on botnet Command & Control (C&C) servers associated with Dridex, Emotes (aka Heodo), TrickBot, QakBot and BazarLoader/BazarBackdoor. This is achieved by providing a database of the C&C servers that security analysts can search through and investigate any suspicious IP addresses they have come across. Additionally, they provide various IP and IOC blocklists and mitigation information to be used to prevent botnet infections.

### [SSL Blacklist](https://sslbl.abuse.ch/)
Abuse.ch developed this tool to identify and detect malicious SSL connections. From these connections, SSL certificates used by botnet C2 servers would be identified and updated on a denylist that is provided for use. The denylist is also used to identify JA3 fingerprints that would help detect and block malware botnet C2 communications on the TCP layer.

You can browse through the SSL certificates and JA3 fingerprints lists or download them to add to your deny list or threat hunting rulesets.

### [URLhaus](https://urlhaus.abuse.ch/)
As the name points out, this tool focuses on sharing malicious URLs used for malware distribution. As an analyst, you can search through the database for domains, URLs, hashes and filetypes that are suspected to be malicious and validate your investigations.

The tool also provides feeds associated with country, AS number and Top Level Domain that an analyst can generate based on specific search needs.

### [ThreatFox](https://threatfox.abuse.ch/)
With ThreatFox,  security analysts can search for, share and export indicators of compromise associated with malware. IOCs can be exported in various formats such as MISP events, Suricata IDS Ruleset, Domain Host files, DNS Response Policy Zone, JSON files and CSV files.

---

## [Task 5  PhishTool]()

Email phishing is one of the main precursors of any cyber attack. Unsuspecting users get duped into the opening and accessing malicious files and links sent to them by email, as they appear to be legitimate. As a result, adversaries infect their victims’ systems with malware, harvesting their credentials and personal data and performing other actions such as financial fraud or conducting ransomware attacks.

For more information and content on phishing, check out these rooms:

- [Phishing Emails 1](https://tryhackme.com/room/phishingemails1tryoe)
- [Phishing Emails 2](https://tryhackme.com/room/phishingemails2rytmuv)
- [Phishing Emails 3](https://tryhackme.com/room/phishingemails3tryoe)
- [Phishing Emails 4](https://tryhackme.com/room/phishingemails4gkxh)
- [Phishing Emails 5](https://tryhackme.com/room/phishingemails5fgjlzxc)

[PhishTool](https://www.phishtool.com/) seeks to elevate the perception of phishing as a severe form of attack and provide a responsive means of email security. Through email analysis, security analysts can uncover email IOCs, prevent breaches and provide forensic reports that could be used in phishing containment and training engagements.

PhishTool has two accessible versions: Community and Enterprise. We shall mainly focus on the Community version and the core features in this task. Sign up for an account via this [link](https://app.phishtool.com/sign-up/community) to use the tool.

The core features include:

- **Perform email analysis**: PhishTool retrieves metadata from phishing emails and provides analysts with the relevant explanations and capabilities to follow the email’s actions, attachments, and URLs to triage the situation.
- **Heuristic intelligence**: OSINT is baked into the tool to provide analysts with the intelligence needed to stay ahead of persistent attacks and understand what TTPs were used to evade security controls and allow the adversary to social engineer a target.
- **Classification and reporting**: Phishing email classifications are conducted to allow analysts to take action quickly. Additionally, reports can be generated to provide a forensic record that can be shared.

Additional features are available on the Enterprise version:

- Manage user-reported phishing events.
- Report phishing email findings back to users and keep them engaged in the process.
- Email stack integration with Microsoft 365 and Google Workspace.

We are presented with an upload file screen from the Analysis tab on login. Here, we submit our email for analysis in the stated file formats. Other tabs include:

- **History**: Lists all submissions made with their resolutions.
- **In-tray**: An Enterprise feature used to receive and process phish reports posted by team members through integrating Google Workspace and Microsoft 365.

![image](https://user-images.githubusercontent.com/51442719/201490649-010cfe9b-93e2-440c-bcb6-3a76565b2061.png)

## Analysis Tab
Once uploaded, we are presented with the details of our email for a more in-depth look. Here, we have the following tabs:

- **Headers**: Provides the routing information of the email, such as source and destination email addresses, Originating IP and DNS addresses and Timestamp.
- **Received Lines**: Details on the email traversal process across various SMTP servers for tracing purposes.
- **X-headers**: These are extension headers added by the recipient mailbox to provide additional information about the email.
- **Security**: Details on email security frameworks and policies such as Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM) and Domain-based Message Authentication, Reporting and Conformance (DMARC).
- **Attachments**: Lists any file attachments found in the email.
- **Message URLs**: Associated external URLs found in the email will be found here.

We can further perform lookups and flag indicators as malicious from these options.  
On the right-hand side of the screen, we are presented with the Plaintext and Source details of the email.

![image](https://user-images.githubusercontent.com/51442719/201490676-56422eaa-9f2b-44a3-8edf-b8656d271a4f.png)

Above the Plaintext section, we have a Resolve checkmark. Here, we get to perform the resolution of our analysis by classifying the email, setting up flagged artefacts and setting the classification codes. Once the email has been classified, the details will appear on the Resolution tab on the analysis of the email.

![image](https://user-images.githubusercontent.com/51442719/201490692-f7d3f51f-2590-4dc5-a011-774bc7b6ec2a.png)

## Scenario:
You are a SOC Analyst and have been tasked to analyse a suspicious email Email1.eml. Use the tool and skills learnt on this task to answer the questions.


---

## [Task 6  Cisco Talos Intelligence]()

IT and Cybersecurity companies collect massive amounts of information that could be used for threat analysis and intelligence. Being one of those companies, Cisco assembled a large team of security practitioners called Cisco Talos to provide actionable intelligence, visibility on indicators, and protection against emerging threats through data collected from their products. The solution is accessible as [Talos Intelligence](https://talosintelligence.com/).

Cisco Talos encompasses six key teams:

- Threat Intelligence & Interdiction: Quick correlation and tracking of threats provide a means to turn simple IOCs into context-rich intel.
- Detection Research: Vulnerability and malware analysis is performed to create rules and content for threat detection.
- Engineering & Development: Provides the maintenance support for the inspection engines and keeps them up-to-date to identify and triage emerging threats.
- Vulnerability Research & Discovery: Working with service and software vendors to develop repeatable means of identifying and reporting security vulnerabilities.
- Communities: Maintains the image of the team and the open-source solutions.
- Global Outreach: Disseminates intelligence to customers and the security community through publications.

More information about Cisco Talos can be found on their [White Paper](https://www.talosintelligence.com/docs/Talos_WhitePaper.pdf)

## Talos Dashboard
Accessing the open-source solution, we are first presented with a reputation lookup dashboard with a world map. This map shows an overview of email traffic with indicators of whether the emails are legitimate, spam or malware across numerous countries. Clicking on any marker, we see more information associated with IP and hostname addresses, volume on the day and the type.

![image](https://user-images.githubusercontent.com/51442719/201544491-43e99568-88fd-4b81-a831-6366458ee5aa.png)

At the top, we have several tabs that provide different types of intelligence resources. The primary tabs that an analyst would interact with are:

- `Vulnerability Information`: Disclosed and zero-day vulnerability reports marked with CVE numbers and CVSS scores. Details of the vulnerabilities reported are provided when you select a specific report, including the timeline taken to get the report published. Microsoft vulnerability advisories are also provided, with the applicable snort rules that can be used.

![image](https://user-images.githubusercontent.com/51442719/201544503-88e37a02-f211-49a1-a3bc-edea900c3635.png)

- `Reputation Center`: Provides access to searchable threat data related to IPs and files using their SHA256 hashes. Analysts would rely on these options to conduct their investigations. Additional email and spam data can be found under the Email & Spam Data tab.

![image](https://user-images.githubusercontent.com/51442719/201544516-5551ac2f-f3f1-41a4-9f68-6ee54af47ee7.png)

![image](https://user-images.githubusercontent.com/51442719/201544522-705061b4-cf76-439f-8733-ab861a1595ac.png)

#### Task
- Use the .eml file you’ve downloaded in the previous task, PhishTool, to answer the following questions.


---

## [Task 7  Scenario 1]()

---

## [Task 8  Scenario 2]()

---

## [Task 9  Conclusion]()
