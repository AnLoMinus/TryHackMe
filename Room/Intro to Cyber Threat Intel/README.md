![image](https://user-images.githubusercontent.com/51442719/197340016-7d4b1477-0002-40d0-9011-7ccd70d754f6.png)

# [Intro to Cyber Threat Intel](https://tryhackme.com/room/cyberthreatintel) | ![image](https://user-images.githubusercontent.com/51442719/197340036-72b1736c-219d-4191-b0a7-aa3a055ff9ab.png)


- [x] [Task 1  Introduction](#task-1--introduction)
- [ ] [Task 2  Cyber Threat Intelligence](#task-2--cyber-threat-intelligence)
- [ ] [Task 3  CTI Lifecycle](#task-3--cti-lifecycle)
- [ ] [Task 4  CTI Standards & Frameworks](#task-4--cti-standards--frameworks)
- [ ] [Task 5  Practical Analysis](#task-5--practical-analysis)


---

- ## Task 1  Introduction

### Introduction
This room will introduce you to cyber threat intelligence (CTI) and various frameworks used to share intelligence.  
As security analysts, CTI is vital for investigating and reporting against adversary attacks with organisational stakeholders and external communities.

### Learning Objectives
The basics of CTI and its various classifications.
The lifecycle followed to deploy and use intelligence during threat investigations.
Frameworks and standards used in distributing intelligence.

### Cyber Threat Intelligence Module
﻿This is the first room in a new Cyber Threat Intelligence module.  
The module will also contain:

- [Threat Intelligence Tools](https://tryhackme.com/room/threatinteltools)
- [YARA](https://tryhackme.com/room/yara)
- [OpenCTI](https://tryhackme.com/room/opencti)
- [MISP](https://tryhackme.com/room/misp)

---

- ## Task 2  Cyber Threat Intelligence

Cyber Threat Intelligence (CTI) can be defined as evidence-based knowledge about adversaries, including their indicators, tactics, motivations, and actionable advice against them.  
These can be utilised to protect critical assets and inform cybersecurity teams and management business decisions.

It would be typical to use the terms “data”, “information”, and “intelligence” interchangeably.  
However, let us distinguish between them to understand better how CTI comes into play.  
An image depicting data from the web, servers and firewalls being collected through a funnel and being sorted.
![image](https://user-images.githubusercontent.com/51442719/197340036-72b1736c-219d-4191-b0a7-aa3a055ff9ab.png)

- **Data**: Discrete indicators associated with an adversary such as IP addresses, URLs or hashes.

- **Information**: A combination of multiple data points that answer questions such as “How many times have employees accessed tryhackme.com within the month?”

- **Intelligence**: The correlation of data and information to extract patterns of actions based on contextual analysis.

The primary goal of CTI is to understand the relationship between your operational environment and your adversary and how to defend your environment against any attacks.  
You would seek this goal by developing your cyber threat context by trying to answer the following questions:

- Who’s attacking you?
- What are their motivations?
- What are their capabilities?
- What artefacts and indicators of compromise (IOCs) should you look out for?

With these questions, threat intelligence would be gathered from different sources under the following categories:

- **Internal**:
  - Corporate security events such as vulnerability assessments and incident response reports.
  - Cyber awareness training reports.
  - System logs and events.
- **Community**:
  - Open web forums.
  - Dark web communities for cybercriminals.
- **External**
  - Threat intel feeds (Commercial & Open-source)
  - Online marketplaces.
  - Public sources include government data, publications, social media, financial and industrial assessments.

###  Threat Intelligence Classifications:
Threat Intel is geared towards understanding the relationship between your operational environment and your adversary.   
With this in mind, we can break down threat intel into the following classifications:

- **Strategic Intel**: High-level intel that looks into the organisation’s threat landscape and maps out the risk areas based on trends, patterns and emerging threats that may impact business decisions.

- **Technical Intel**: Looks into evidence and artefacts of attack used by an adversary. Incident Response teams can use this intel to create a baseline attack surface to analyse and develop defence mechanisms.

- **Tactical Intel**: Assesses adversaries’ tactics, techniques, and procedures (TTPs). This intel can strengthen security controls and address vulnerabilities through real-time investigations.

- **Operational Intel**: Looks into an adversary’s specific motives and intent to perform an attack. Security teams may use this intel to understand the critical assets available in the organisation (people, processes and technologies) that may be targeted.

---

- ## Task 3  CTI Lifecycle

---

- ## Task 4  CTI Standards & Frameworks

---

- ## Task 5  Practical Analysis
