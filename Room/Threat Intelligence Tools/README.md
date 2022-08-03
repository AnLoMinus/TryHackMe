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

---

## [Task 5  PhishTool]()

---

## [Task 6  Cisco Talos Intelligence]()

---

## [Task 7  Scenario 1]()

---

## [Task 8  Scenario 2]()

---

## [Task 9  Conclusion]()
