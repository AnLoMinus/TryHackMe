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
OpenCTI uses a variety of knowledge schemas in structuring data, the main one being the Structured Threat Information Expression (STIX2) standards. STIX is a serialised and standardised language format used in threat intelligence exchange. It allows for the data to be implemented as entities and relationships, effectively tracing the origin of the provided information.

This data model is supported by how the platform's architecture has been laid out. The image below gives an architectural structure for your know-how.

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

---

## Task 5  OpenCTI Dashboard 2

---

## Task 6  Investigative Scenario

---

## Task 7  Room Conclusion

---
