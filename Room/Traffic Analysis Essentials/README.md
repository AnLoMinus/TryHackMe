# [Traffic Analysis Essentials](https://tryhackme.com/room/trafficanalysisessentials)
![image](https://user-images.githubusercontent.com/51442719/200156840-7e69feca-a4a5-4fad-8159-cd19a9a80298.png)
> ### Learn Network Security and Traffic Analysis foundations and take a step into probing network anomalies.

- [ ] [Task 1  Introduction](#)
- [ ] [Task 2  Network Security and Network Data](#)
- [ ] [Task 3  Traffic Analysis](#)
- [ ] [Task 4  Conclusion](#)

---

# Task 1  Introduction

Network Security is a set of operations for protecting data, applications, devices and systems connected to the network.  
It is accepted as one of the significant subdomains of cyber security.  
It focuses on the system design, operation and management of the architecture/infrastructure to provide network accessibility, integrity, continuity and reliability.  
Traffic analysis (often called Network Traffic Analysis) is a subdomain of the Network Security domain, and its primary focus is investigating the network data to identify problems and anomalies. 

This room will cover the foundations of Network Security and Traffic analysis and introduce the essential concepts of these disciplines to help you step into Traffic/Packet Analysis.   
We suggest completing the "[Network Fundamentals](https://tryhackme.com/module/network-fundamentals)" module before starting working in this room.  

---

# Task 2  Network Security and Network Data

![image](https://user-images.githubusercontent.com/51442719/200157013-240f4f8d-a061-45b7-b7f3-1f197c5ac5c6.png)

## Network Security

The essential concern of Network Security focuses on two core concepts: authentication and authorisation.  
There are a variety of tools, technologies, and approaches to ensure and measure implementations of these two key concepts and go beyond to provide continuity and reliability.  
Network security operations contain three base control levels to ensure the maximum available security management.

**Base Network Security Control Levels:**

| Physical | Physical security controls prevent unauthorised physical access to networking devices, cable boards, locks, and all linked components. |
|---|---|
| Technical | Data security controls prevent unauthorised access to network data, like installing tunnels and implementing security layers. |
| Administrative | Administrative security controls provide consistency in security operations like creating policies, access levels and authentication processes. |

There are two main approaches and multiple elements under these control levels. The most common elements used in network security operations are explained below.

**The main approaches:**

| Access Control | Threat Control |
|:---:|:---:|
| The starting point of Network Security. It is a set of controls to ensure authentication and authorisation.  | Detecting and preventing anomalous/malicious activities on the network. It contains both internal (trusted) and external traffic data probes. |


**The key elements of Access Control:**

| Firewall Protection | Controls incoming and outgoing network traffic with predetermined security rules. Designed to block suspicious/malicious traffic and application-layer threats while allowing legitimate and expected traffic. |
|---|---|
| Network Access Control (NAC) | Controls the devices' suitability before access to the network. Designed to verify device specifications and conditions are compliant with the predetermined profile before connecting to the network. |
| Identity and Access Management (IAM) | Controls and manages the asset identities and user access to data systems and resources over the network. |
| Load Balancing | Controls the resource usage to distribute (based on metrics) tasks over a set of resources and improve overall data processing flow. |
| Network Segmentation | Creates and controls network ranges and segmentation to isolate the users' access levels, group assets with common functionalities, and improve the protection of sensitive/internal devices/data in a safer network. |
| Virtual Private Networks (VPN) | Creates and controls encrypted communication between devices (typically for secure remote access) over the network (including communications over the internet). |
| Zero Trust Model | Suggests configuring and implementing the access and permissions at a minimum level (providing access required to fulfil the assigned role). The mindset is focused on: "Never trust, always verify". |

**The key elements of Threat Control:**

| Intrusion Detection and Prevention (IDS/IPS) | Inspects the traffic and creates alerts (IDS) or resets the connection (IPS) when detecting an anomaly/threat. |
|---|---|
| Data Loss Prevention (DLP) | Inspects the traffic (performs content inspection and contextual analysis of the data on the wire) and blocks the extraction of sensitive data. |
| Endpoint Protection | Protecting all kinds of endpoints and appliances that connect to the network by using a multi-layered approach like encryption, antivirus, antimalware, DLP, and IDS/IPS. |
| Cloud Security | Protecting cloud/online-based systems resources from threats and data leakage by applying suitable countermeasures like VPN and data encryption. |
| Security Information and Event Management (SIEM) | Technology that helps threat detection, compliance, and security incident management, through available data (logs and traffic statistics) by using event and context analysis to identify anomalies, threats, and vulnerabilities. |
| Security Orchestration Automation and Response (SOAR) | Technology that helps coordinate and automates tasks between various people, tools, and data within a single platform to identify anomalies, threats, and vulnerabilities. It also supports vulnerability management, incident response, and security operations. |
| Network Traffic Analysis & Network Detection and Response | Inspecting network traffic or traffic capture to identify anomalies and threats. |

**Typical Network Security Management Operation is explained in the given table:**

| Deployment | Configuration | Management | Monitoring | Maintenance |
|:---:|:---:|:---:|:---:|:---:|
| Device and software installation <br> Initial configuration Automation | Feature configuration Initial network access configuration | Security policy implementation NAT and VPN implementation Threat mitigation | System monitoring User activity monitoring Threat monitoring  Log and traffic sample capturing | Upgrades Security updates Rule adjustments Licence management Configuration updates |



---

# Task 3  Traffic Analysis

---

# Task 4  Conclusion
