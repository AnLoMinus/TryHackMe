![image](https://user-images.githubusercontent.com/51442719/201569595-69470ebd-add7-496c-b1e9-cd56d223a076.png)

# [OpenCTI](https://tryhackme.com/room/opencti)  
### Provide an understanding of the OpenCTI Project

---

- [Task 1  Room Overview](#)
- [Task 2  Introduction to OpenCTI](#)
- [Task 3  OpenCTI Data Model](#)
- [Task 4  OpenCTI Dashboard 1](#)
- [Task 5  OpenCTI Dashboard 2](#)
- [Task 6  Investigative Scenario](#)
- [Task 7  Room Conclusion](#)

---

## Task 1  Room Overview

This room will cover the concepts and usage of OpenCTI, an open-source threat intelligence platform. The room will help you understand and answer the following questions:

What is OpenCTI and how is it used?
How would I navigate through the platform?
What functionalities will be important during a security threat analysis?
Prior to going through this room, we recommend checking out these rooms as prerequisites:

- [MITRE ATT&CK Framework](https://tryhackme.com/room/mitre)
- [TheHive](https://tryhackme.com/room/thehiveproject)
- [MISP](https://tryhackme.com/room/misp)
- [Threat Intelligence Tools](http://tryhackme.com/room/threatinteltools)

![image](https://user-images.githubusercontent.com/51442719/201573314-f839c932-4d2e-4e18-99a1-ccb85c69e77b.png)

---

## Task 2  Introduction to OpenCTI

Cyber Threat Intelligence is typically a managerial mystery to handle, with organisations battling with how to input, digest, analyse and present threat data in a way that will make sense. From the rooms that have been linked on the overview, it is clear that there are numerous platforms that have been developed to tackle the juggernaut that is Threat Intelligence.

### OpenCTI
[OpenCTI](https://www.opencti.io/) is another open-sourced platform designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs.

### Objective
Developed by the collaboration of the [French National cybersecurity agency (ANSSI)](https://www.ssi.gouv.fr/), the platform's main objective is to create a comprehensive tool that allows users to capitalise on technical and non-technical information while developing relationships between each piece of information and its primary source. The platform can use the [MITRE ATT&CK framework](https://tryhackme.com/room/mitre) to structure the data. Additionally, it can be integrated with other threat intel tools such as MISP and TheHive. Rooms to these tools have been linked in the overview.

![image](https://user-images.githubusercontent.com/51442719/201573495-b4625985-b542-4870-a0cf-851a36b02db9.png)

---

## Task 3  OpenCTI Data Model

### OpenCTI Data Model
OpenCTI uses a variety of knowledge schemas in structuring data, the main one being the Structured Threat Information Expression ([STIX2](https://oasis-open.github.io/cti-documentation/stix/intro)) standards. STIX is a serialised and standardised language format used in threat intelligence exchange. It allows for the data to be implemented as entities and relationships, effectively tracing the origin of the provided information.

This data model is supported by how the platform's architecture has been laid out. The image below gives an architectural structure for your know-how.

![image](https://user-images.githubusercontent.com/51442719/201573959-e48817a1-9a17-4225-afc0-f3f6acabc2bd.png)

> Source: [OpenCTI Public Knowledge Base](https://luatix.notion.site/OpenCTI-Public-Knowledge-Base-d411e5e477734c59887dad3649f20518)

The highlight services include:

- GraphQL API: The API connects clients to the database and the messaging system.
- Write workers: Python processes utilised to write queries asynchronously from the RabbitMQ messaging system.
- Connectors: Another set of python processes used to ingest, enrich or export data on the platform. These connectors provide the application with a robust network of integrated systems and frameworks to create threat intelligence relations and allow users to improve their defence tactics.

According to OpenCTI, connectors fall under the following classes:

| Class | Description | Examples |
|:---:|:---:|:---:|
| External Input Connector | Ingests information from external sources | CVE, MISP, TheHive, MITRE |
| Stream Connector | Consumes platform data stream | History, Tanium |
| Internal Enrichment Connector | Takes in new OpenCTI entities from user requests | Observables enrichment |
| Internal Import File Connector | Extracts information from uploaded reports | PDFs, STIX2 Import |
| Internal Export File Connector | Exports information from OpenCTI into different file formats | CSV, STIX2 export, PDF |

Refer to the [connectors](https://github.com/OpenCTI-Platform/connectors) and [data model](https://luatix.notion.site/Data-model-4427344d93a74fe194d5a52ce4a41a8d) documentation for more details on configuring connectors and the data schema.

---

## Task 4  OpenCTI Dashboard 1

Follow along with the task by launching the attached machine and using the credentials provided; log in to the OpenCTI Dashboard via the AttackBox on http://10.10.25.103:8080/. Give the machine 5 minutes to start up and it is advisable to use the AttackBox on fullscreen.

- Username: 
  - info@tryhack.io
- Password: 
  - TryHackMe1234

### OpenCTI Dashboard
Once connected to the platform, the opening dashboard showcases various visual widgets summarising the threat data ingested into OpenCTI. Widgets on the dashboard showcase the current state of entities ingested on the platform via the total number of entities, relationships, reports and observables ingested, and changes to these properties noted within 24 hours.

![image](https://user-images.githubusercontent.com/51442719/201574511-72ce93ad-cbdd-45d5-bf94-7cf368b875e1.png)

### Activities & Knowledge
The OpenCTI categorises and presents entities under the Activities and Knowledge groups on the left-side panel. The activities section covers security incidents ingested onto the platform in the form of reports. It makes it easy for analysts to investigate these incidents. In contrast, the Knowledge section provides linked data related to the tools adversaries use, targeted victims and the type of threat actors and campaigns used.

### Analysis
The Analysis tab contains the input entities in reports analysed and associated external references. Reports are central to OpenCTI as knowledge on threats and events are extracted and processed. They allow for easier identification of the source of information by analysts. Additionally, analysts can add their investigation notes and other external resources for knowledge enrichment. As displayed below, we can look at the Triton Software report published by MITRE ATT&CK and observe or add to the details provided.

![image](https://user-images.githubusercontent.com/51442719/201574556-ac01724a-f830-40c8-8f48-da1be504202a.png)

### Events
Security analysts investigate and hunt for events involving suspicious and malicious activities across their organisational network. Within the Events tab, analysts can record their findings and enrich their threat intel by creating associations for their incidents.

![image](https://user-images.githubusercontent.com/51442719/201574574-b4fe4cdd-1241-4fe3-96c4-3308b63b64f8.png)

### Observations
Technical elements, detection rules and artefacts identified during a cyber attack are listed under this tab: one or several identifiable makeup indicators. These elements assist analysts in mapping out threat events during a hunt and perform correlations between what they observe in their environments against the intel feeds. 

![image](https://user-images.githubusercontent.com/51442719/201574591-02261fd3-21da-4b96-bb92-4e211116333b.png)

### Threats
All information classified as threatening to an organisation or information would be classified under threats. These will include:

- Threat Actors: An individual or group of attackers seeking to propagate malicious actions against a target.

- Intrusion Sets: An array of TTPs, tools, malware and infrastructure used by a threat actor against targets who share some attributes. APTs and threat groups are listed under this category on the platform due to their known pattern of actions.

- Campaigns: Series of attacks taking place within a given period and against specific victims initiated by advanced persistent threat actors who employ various TTPs. Campaigns usually have specified objectives and are orchestrated by threat actors from a nation state, crime syndicate or other disreputable organisation.

![image](https://user-images.githubusercontent.com/51442719/201574636-64e6f5e1-c4a8-4603-b3d9-7c45a9f10709.png)

### Arsenal
This tab lists all items related to an attack and any legitimate tools identified from the entities.

- Malware: Known and active malware and trojan are listed with details of their identification and mapping based on the knowledge ingested into the platform. In our example, we analyse the 4H RAT malware and we can extract information and associations made about the malware.

- Attack Patterns: Adversaries implement and use different TTPs to target, compromise, and achieve their objectives. Here, we can look at the details of the Command-Line Interface and make decisions based on the relationships established on the platform and navigate through an investigation associated with the technique.

- Courses of Action: MITRE maps out concepts and technologies that can be used to prevent an attack technique from being employed successfully. These are represented as Courses of Action (CoA) against the TTPs.

- Tools: Lists all legitimate tools and services developed for network maintenance, monitoring and management. Adversaries may also use these tools to achieve their objectives. For example, for the Command-Line Interface attack pattern, it is possible to narrow down that CMD would be used as an execution tool. As an analyst, one can investigate reports and instances associated with the use of the tool.

- Vulnerabilities: Known software bugs, system weaknesses and exposures are listed to provide enrichment for what attackers may use to exploit and gain access to systems. The Common Vulnerabilities and Exposures (CVE) list maintained by MITRE is used and imported via a connector.

![image](https://user-images.githubusercontent.com/51442719/201574682-09a4cb4f-7ffe-4b33-ba70-30f76e812ae0.png)

### Entities
This tab categorises all entities based on operational sectors, countries, organisations and individuals. This information allows for knowledge enrichment on attacks, organisations or intrusion sets.

![image](https://user-images.githubusercontent.com/51442719/201574712-fd5b6be7-fa46-41c8-a1f9-85ceec787bc2.png)


---

## Task 5  OpenCTI Dashboard 2

---

## Task 6  Investigative Scenario

---

## Task 7  Room Conclusion

---
