![image](https://user-images.githubusercontent.com/51442719/181074765-a333fb74-1e8d-481c-880e-ce925d73b707.png)
![image](https://user-images.githubusercontent.com/51442719/181074783-88591fb5-b5b9-4051-be20-2cf8ce86cdbb.png)
# [Zeek](https://tryhackme.com/room/zeekbro)
## Introduction to hands-on network monitoring and threat detection with Zeek (formerly Bro).
### Zeek (formerly Bro) is an open-source and commercial network monitoring tool (traffic analyser).
- [The official description](https://docs.zeek.org/en/master/about.html); "Zeek (formerly Bro) is the world's leading platform for network security monitoring. 
- Flexible, open-source, and powered by defenders." "Zeek is a passive, open-source network traffic analyser. 
- Many operators use Zeek as a network security monitor (NSM) to support suspicious or malicious activity investigations. 
- Zeek also supports a wide range of traffic analysis tasks beyond the security domain, including performance measurement and troubleshooting."

---

- [x] [Task 1  Introduction](#task-1--introduction)
- [ ] [Task 2  Network Security Monitoring and Zeek](#task-2--network-security-monitoring-and-zeek)
- [ ] [Task 3  Zeek Logs](#task-3--zeek-logs)
- [ ] [Task 4  CLI Kung-Fu Recall: Processing Zeek Logs](#task-4--cli-kung-fu-recall-processing-zeek-logs)
- [ ] [Task 5  Zeek Signatures](#task-5--zeek-signatures)
- [ ] [Task 6  Zeek Scripts | Fundamentals](#task-6--zeek-scripts--fundamentals)
- [ ] [Task 7  Zeek Scripts | Scripts and Signatures](#task-7--zeek-scripts--scripts-and-signatures)
- [ ] [Task 8  Zeek Scripts | Frameworks](#task-8--zeek-scripts--frameworks)
- [ ] [Task 9  Zeek Scripts | Packages](#task-9--zeek-scripts--packages)
- [ ] [Task 10  Conclusion](#task-10--conclusion)

---

## [Task 1  Introduction]()

- The room aims to provide a general network monitoring overview and work with Zeek to investigate captured traffic. 
- This room will expect you to have basic Linux familiarity and Network fundamentals (ports, protocols and traffic data). 
- We suggest completing the "[Network Fundamentals](https://tryhackme.com/module/network-fundamentals)" path before starting working in this room. 

- A VM is attached to this room. 
- You don't need SSH or RDP; the room provides a "Split View" feature. 
- Exercise files are located in the folder on the desktop. 
- Log cleaner script "clear-logs.sh" is available in each exercise folder.
  > ![image](https://user-images.githubusercontent.com/51442719/181075348-8907645f-fa37-4b73-9e60-241f0608caa0.png)

### Answer the questions below
- Read the task above.
  > `No answer needed`
  

---

## [Task 2  Network Security Monitoring and Zeek]()
  > ![image](https://user-images.githubusercontent.com/51442719/181076740-05a4157d-23b9-48e6-86fb-82d39c2812f9.png)

### Introduction to Network Monitoring Approaches
- Network monitoring is a set of management actions to watch/continuously overview and optionally save the network traffic for further investigation. 
- This action aims to detect and reduce network problems, improve performance, and in some cases, increase overall productivity. 
- It is a main part of the daily IT/SOC operations and differs from Network Security Monitoring (NSM) in its purpose.

#### Network Monitoring
- Network monitoring is highly focused on IT assets like uptime (availability), device health and connection quality (performance), and network traffic balance and management (configuration). 
- Monitoring and visualising the network traffic, troubleshooting, and root cause analysis are also part of the Network Monitoring process. 
- This model is helpful for network administrators and usually doesn't cover identifying non-asset in-depth vulnerabilities and significant security concerns like internal threats and zero-day vulnerabilities. 
- Usually, Network Monitoring is not within the SOC scope. 
- It is linked to the enterprise IT/Network management team.

#### Network Security Monitoring
- Network Security Monitoring is focused on network anomalies like rogue hosts, encrypted traffic, suspicious service and port usage, and malicious/suspicious traffic patterns in an intrusion/anomaly detection and response approach. 
- Monitoring and visualising the network traffic and investigating suspicious events is a core part of Network Security Monitoring. 
- This model is helpful for security analysts/incident responders, security engineers and threat hunters and covers identifying threats, vulnerabilities and security issues with a set of rules, signatures and patterns. 
- Network Security Monitoring is part of the SOC, and the actions are separated between tier 1-2-3 analyst levels.

### What is ZEEK?
- Zeek (formerly Bro) is an open-source and commercial passive Network Monitoring tool (traffic analysis framework) developed by Lawrence Berkeley Labs.
- Today, Zeek is supported by several developers, and Corelight provides an Enterprise-ready fork of Zeek. 
- Therefore this tool is called both open source and commercial. 
- The differences between the open-source version and the commercial version are detailed [here](https://corelight.com/products/compare-to-open-source-zeek?hsLang=en).
- Zeek differs from known monitoring and IDS/IPS tools by providing a wide range of detailed logs ready to investigate both for forensics and data analysis actions. 
- Currently, Zeek provides 50+ logs in 7 categories.

### Zeek vs Snort
- While both are called IDS/NIDS, it is good to know the cons and pros of each tool and use them in a specific manner. 
- While there are some overlapping functionalities, they have different purposes for usage.


---

## [Task 3  Zeek Logs]()

---

## [Task 4  CLI Kung-Fu Recall: Processing Zeek Logs]()

---

## [Task 5  Zeek Signatures]()

---

## [Task 6  Zeek Scripts | Fundamentals]()

---

## [Task 7  Zeek Scripts | Scripts and Signatures]()

---

## [Task 8  Zeek Scripts | Frameworks]()

---

## [Task 9  Zeek Scripts | Packages]()

---

## [Task 10  Conclusion]()

---
