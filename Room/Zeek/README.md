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

- (`NSM`) - Network Security Monitoring 
- (`SOC`) – Security Operating Center

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

#### Available Frameworks

| Tool | Zeek | Snort |
|:---:|:---:|:---:|
| Capabilities | NSM and IDS framework. It is heavily focused on network analysis. It is more focused on specific threats to trigger alerts. The detection mechanism is focused on events. | An IDS/IPS system. It is heavily focused on signatures to detect vulnerabilities. The detection mechanism is focused on signature patterns and packets. |
| Cons | Hard to use. The analysis is done out of the Zeek, manually or by automation.  | Hard to detect complex threats. |
| Pros | It provides in-depth traffic visibility. Useful for threat hunting. Ability to detect complex threats. It has a scripting language and supports event correlation.  Easy to read logs. | Easy to write rules. Cisco supported rules. Community support. |
| Common Use Case | Network monitoring. In-depth traffic investigation. Intrusion detecting in chained events.  | Intrusion detection and prevention. Stop known attacks/threats. |

- You can read more on frameworks [`here`](https://docs.zeek.org/en/master/frameworks/index.html). 

### Zeek Outputs
- As mentioned before, Zeek provides 50+ log files under seven different categories, which are helpful in various areas such as traffic monitoring, intrusion detection, threat hunting and web analytics. 
- This section is not intended to discuss the logs in-depth. The logs are covered in TASK 3.
- Once you run Zeek, it will automatically start investigating the traffic or the given pcap file and generate logs automatically. 
- Once you process a pcap with Zeek, it will create the logs in the working directory. 
- If you run the Zeek as a service, your logs will be located in the default log path. 
- The default log path is: `/opt/zeek/logs/`

### Working with Zeek
- There are two operation options for Zeek. 
- The first one is running it as a service, and the second option is running the Zeek against a pcap. 
- Before starting working with Zeek, let's check the version of the Zeek instance with the following command: `zeek -v`
- Now we are sure that we have Zeek installed. 
- Let's start the Zeek as a service! To do this, we need to use the "ZeekControl" module, as shown below. 
- The "ZeekControl" module requires superuser permissions to use. 
- You can elevate the session privileges and switch to the superuser account to examine the generated log files with the following command: `sudo su`
- Here we can manage the Zeek service and view the status of the service. 
- Primary management of the Zeek service is done with three commands; "status", "start", and "stop". 
```cmd
root@ubuntu$ zeekctl
Welcome to ZeekControl 2.X.0
[ZeekControl] > status
Name         Type       Host          Status    Pid    Started
zeek         standalone localhost     stopped
[ZeekControl] > start
starting zeek ...
[ZeekControl] > status
Name         Type       Host          Status    Pid    Started
zeek         standalone localhost     running   2541   13 Mar 18:25:08
[ZeekControl] > stop
stopping zeek ...
[ZeekControl] > status
Name         Type       Host          Status    Pid    Started
zeek         standalone localhost     stopped
```

- You can also use the "ZeekControl" mode with the following commands as well;
  - `zeekctl status`
  - `zeekctl start` 
  - `zeekctl stop`
- The only way to listen to the live network traffic is using Zeek as a service. 
- Apart from using the Zeek as a network monitoring tool, we can also use it as a packet investigator. 
- To do so, we need to process the pcap files with Zeek, as shown below. 
- Once you process a pcap file, Zeek automatically creates log files according to the traffic.
- In pcap processing mode, logs are saved in the working directory. 
- You can view the generated logs using the `ls -l` command.  
```cmd
root@ubuntu$ zeek -C -r sample.pcap 

root@ubuntu$ ls -l
-rw-r--r-- 1 ubuntu ubuntu  11366 Mar 13 20:45 conn.log
-rw-r--r-- 1 ubuntu ubuntu    763 Mar 13 20:45 dhcp.log
-rw-r--r-- 1 ubuntu ubuntu   2918 Mar 13 20:45 dns.log
-rw-r--r-- 1 ubuntu ubuntu    254 Mar 13 20:45 packet_filter.log 
```
- Main Zeek command line parameters are explained below;

| Parameter | Description |
|:---:|:---:|
| -r |  Reading option, read/process a pcap file. |
| -C |  Ignoring checksum errors. |
| -v |  Version information. |
| zeekctl | ZeekControl module. |

### Zeek Architecture
- Zeek has two primary layers; "Event Engine" and "Policy Script Interpreter". 
- The Event Engine layer is where the packets are processed; it is called the event core and is responsible for describing the event without focusing on event details. 
- It is where the packages are divided into parts such as source and destination addresses, protocol identification, session analysis and file extraction.
- The Policy Script Interpreter layer is where the semantic analysis is conducted. 
- It is responsible for describing the event correlations by using Zeek scripts.

> ![image](https://user-images.githubusercontent.com/51442719/181111656-64f74fbc-2683-4d55-8855-57515223a328.png)

### Zeek Frameworks
- Zeek has several frameworks to provide extended functionality in the scripting layer. 
- These frameworks enhance Zeek's flexibility and compatibility with other network components. 
- Each framework focuses on the specific use case and easily runs with Zeek installation. 
- For instance, we will be using the "Logging Framework" for all cases. 
- Having ide on each framework's functionality can help users quickly identify an event of interest. 

#### Available Frameworks

| Logging | Notice | Input | Configuration | Intelligence |
|:---:|:---:|:---:|:---:|:---:|
| Cluster | Broker Communication | Supervisor | GeoLocation | File Analysis |
| Signature | Summary | NetControl | Packet Analysis | TLS Decryption |


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
