![image](https://user-images.githubusercontent.com/51442719/197387383-c4ea3ff0-60bc-44e7-886c-ed51684ee82d.png)

# [TheHive Project](https://tryhackme.com/room/thehiveproject)
#### Learn how to use TheHive, a Security Incident Response Platform, to report investigation findings

- Task 1 | Room Outline
- Task 2 | Introduction
- Task 3 | TheHive Features & Integrations
- Task 4 | User Profiles & Permissions
- Task 5 | Analyst Interface Navigation
- Task 6 | Room Conclusion

---

- ## Task 1 | Room Outline

Welcome to TheHive Project Outline!

This room will cover the foundations of using the TheHive Project, a Security Incident Response Platform.
Specifically, we will be looking at:

- What TheHive is?
- An overview of the platform's functionalities and integrations.
- Installing TheHive for yourself.
- Navigating the UI.
- Creation of a case assessment.

Before we begin, ensure you download the attached file, as it will be needed for Task 5.

![image](https://user-images.githubusercontent.com/51442719/197387274-20c921d4-080f-4d51-b452-e919cb2d69b4.png)



---

- ## Task 2 | Introduction

TheHive Project is a scalable, open-source and freely available Security Incident Response Platform, designed to assist security analysts and practitioners working in SOCs, CSIRTs and CERTs to track, investigate and act upon identified security incidents in a swift and collaborative manner.

Security Analysts can collaborate on investigations simultaneously, ensuring real-time information pertaining to new or existing cases, tasks, observables and IOCs are available to all team members.

More information about the project can be found on https://thehive-project.org/ & their [GitHub Repo](https://github.com/TheHive-Project/TheHive).

![image](https://user-images.githubusercontent.com/51442719/197387319-2c854ada-2382-4ce7-9556-ab4d590124ea.png)
Image: Cases dashboard on TheHive by order of reported severity


TheHive Project operates under the guide of three core functions:

- **Collaborate**: Multiple analysts from one organisation can work together on the same case simultaneously. Through its live stream capabilities, everyone can keep an eye on the cases in real time.
- **Elaborate**: Investigations correspond to cases. The details of each case can be broken down into associated tasks, which can be created from scratch or through a template engine. Additionally, analysts can record their progress, attach artifacts of evidence and assign tasks effortlessly.
- **Act**: A quick triaging process can be supported by allowing analysts to add observables to their cases, leveraging tags, flagging IOCs and identifying previously seen observables to feed their threat intelligence.


---

- ## Task 3 | TheHive Features & Integrations

TheHive allows analysts from one organisation to work together on the same case simultaneously. This is due to the platform's rich feature set and integrations that support analyst workflows. The features include:

- **Case/Task Management**: Every investigation is meant to correspond to a case that has been created. Each case can be broken down into one or more tasks for added granularity and even be turned into templates for easier management. Additionally, analysts can record their progress, attach pieces of evidence or noteworthy files, add tags and other archives to cases.

- **Alert Triage**: Cases can be imported from SIEM alerts, email reports and other security event sources. This feature allows an analyst to go through the imported alerts and decide whether or not they are to be escalated into investigations or incident response.

- **Observable Enrichment with Cortex**: One of the main feature integrations TheHive supports is Cortex, an observable analysis and active response engine. Cortex allows analysts to collect more information from threat indicators by performing correlation analysis and developing patterns from the cases. More information on [Cortex](https://github.com/TheHive-Project/Cortex/).

- **Active Response**: TheHive allows analysts to use Responders and run active actions to communicate, share information about incidents and prevent or contain a threat.

- **Custom Dashboards**: Statistics on cases, tasks, observables, metrics and more can be compiled and distributed on dashboards that can be used to generate useful KPIs within an organisation.

- **Built-in MISP Integration**: Another useful integration is with [MISP](https://www.misp-project.org/index.html), a threat intelligence platform for sharing, storing and correlating Indicators of Compromise of targeted attacks and other threats. This integration allows analysts to create cases from MISP events, import IOCs or export their own identified indicators to their MISP communities.

Other notable integrations that TheHive supports are [DigitalShadows2TH](https://github.com/TheHive-Project/DigitalShadows2TH) & [ZeroFox2TH](https://github.com/TheHive-Project/Zerofox2TH), free and open-source extensions of alert feeders from [DigitalShadows](https://www.digitalshadows.com/) and [ZeroFox](https://www.zerofox.com/) respectively. These integrations ensure that alerts can be added into TheHive and transformed into new cases using pre-defined incident response templates or by adding to existing cases.


---

- ## Task 4 | User Profiles & Permissions

---

- ## Task 5 | Analyst Interface Navigation

---

- ## Task 6 | Room Conclusion

---
