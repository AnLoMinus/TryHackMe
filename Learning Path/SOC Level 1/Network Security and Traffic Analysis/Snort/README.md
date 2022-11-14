![image](https://user-images.githubusercontent.com/51442719/201674330-21fe17e5-852f-4bdf-924f-28a0f98e2ac2.png)

# [Snort](https://tryhackme.com/room/snort)
### Learn how to use Snort to detect real-time threats, analyse recorded traffic files and identify anomalies.

---

- [Task 1  Introduction](#)
- [Task 2  Interactive Material and VM](#)
- [Task 3  Introduction to IDS/IPS](#)
- [Task 4  First Interaction with Snort](#)
- [Task 5  Operation Mode 1: Sniffer Mode](#)
- [Task 6  Operation Mode 2: Packet Logger Mode](#)
- [Task 7  Operation Mode 3: IDS/IPS](#)
- [Task 8  Operation Mode 4: PCAP Investigation](#)
- [Task 9  Snort Rule Structure](#)
- [Task 10  Snort2 Operation Logic: Points to Remember](#)
- [Task 11  Conclusion](#)

---

## Task 1  Introduction

![image](https://user-images.githubusercontent.com/51442719/201674693-71457bbe-85c0-426a-9f16-418888cbd471.png)

This room expects you to be familiar with basic Linux command-line functionalities like general system navigation and Network fundamentals (ports, protocols and traffic data). The room aims to encourage you to start working with Snort to analyse live and captured traffic.

Before joining this room, we suggest completing the '[Network Fundamentals](https://tryhackme.com/module/network-fundamentals)' module. If you have general knowledge of network basics and Linux fundamentals, you will be ready to begin! If you feel you need assistance in the Linux command line, you can always refer to our "Linux Fundamentals" rooms (here [1](https://tryhackme.com/room/linuxfundamentalspart1) [2](https://tryhackme.com/room/linuxfundamentalspart2) [3](https://tryhackme.com/room/linuxfundamentalspart3)); 

SNORT is an open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS). It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team. 

[The official description](https://www.snort.org/): "Snort is the foremost Open Source Intrusion Prevention System (IPS) in the world. Snort IPS uses a series of rules that help define malicious network activity and uses those rules to find packets that match against them and generate alerts for users."

---

## Task 2  Interactive Material and VM

---

## Task 3  Introduction to IDS/IPS

![image](https://user-images.githubusercontent.com/51442719/201675165-45f20654-a786-4b62-8bf4-9964a25edcc5.png)

Before diving into Snort and analysing traffic, let's have a brief overview of what an Intrusion Detection System (IDS) and Intrusion Prevention System (IPS) is. It is possible to configure your network infrastructure and use both of them, but before starting to use any of them, let's learn the differences.

### Intrusion Detection System (IDS)

IDS is a passive monitoring solution for detecting possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for generating alerts for each suspicious event. 

There are two main types of IDS systems;

- `Network Intrusion Detection System` (`NIDS`) - NIDS monitors the traffic flow from various areas of the network. The aim is to investigate the traffic on the entire subnet. If a signature is identified, an alert is created.
- `Host-based Intrusion Detection System` (`HIDS`) - HIDS monitors the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, an alert is created.

### Intrusion Prevention System (IPS)
IPS is an active protecting solution for preventing possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for stopping/preventing/terminating the suspicious event as soon as the detection is performed.

 There are four main types of IPS systems;

- `Network Intrusion Prevention System` (`NIPS`) - NIPS monitors the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, the connection is terminated.
- `Behaviour-based Intrusion Prevention System` (`Network Behaviour Analysis` - `NBA`) - Behaviour-based systems monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, the connection is terminated.

Network Behaviour Analysis System works similar to NIPS. The difference between NIPS and Behaviour-based is; behaviour based systems require a training period (also known as "baselining") to learn the normal traffic and differentiate the malicious traffic and threats. This model provides more efficient results against new threats.

The system is trained to know the "normal" to detect "abnormal". The training period is crucial to avoid any false positives. In case of any security breach during the training period, the results will be highly problematic. Another critical point is to ensure that the system is well trained to recognise benign activities. 

- `Wireless Intrusion Prevention System` (`WIPS`) - WIPS monitors the traffic flow from of wireless network. The aim is to protect the wireless traffic and stop possible attacks launched from there. If a signature is identified, the connection is terminated.
- `Host-based Intrusion Prevention System` (`HIPS`) - HIPS actively protects the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, the connection is terminated.
HIPS working mechanism is similar to HIDS. The difference between them is that while HIDS creates alerts for threats, HIPS stops the threats by terminating the connection.

### Detection/Prevention Techniques

There are three main detection and prevention techniques used in IDS and IPS solutions;

| Technique | Approach |
|:---:|:---:|
| Signature-Based | This technique relies on rules that identify the specific patterns of the known malicious behaviour. This model helps detect known threats.  |
| Behaviour-Based | This technique identifies new threats with new patterns that pass through signatures. The model compares the known/normal with unknown/abnormal behaviours. This model helps detect previously unknown or new threats. |
| Policy-Based | This technique compares detected activities with system configuration and security policies. This model helps detect policy violations. |

### Summary

Phew! That was a long ride and lots of information. Let's summarise the overall functions of the IDS and IPS in a nutshell.

- `IDS` can identify threats but require user assistance to stop them.
- `IPS` can identify and block the threats with less user assistance at the detection time.

**Now let's talk about Snort. [Here is the rest of the official description](https://www.snort.org/) of the snort;**

> "Snort can be deployed inline to stop these packets, as well. Snort has three primary uses: As a packet sniffer like tcpdump, as a packet logger — which is useful for network traffic debugging, or it can be used as a full-blown network intrusion prevention system. Snort can be downloaded and configured for personal and business use alike."

SNORT is an open-source, rule-based Network Intrusion Detection and Prevention System (`NIDS`/`NIPS`). It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team. 

![image](https://user-images.githubusercontent.com/51442719/201677067-23212e02-0206-49e0-8044-c4db1d5f7c4e.png)

**Capabilities of Snort;**

- Live traffic analysis
- Attack and probe detection
- Packet logging
- Protocol analysis
- Real-time alerting
- Modules & plugins
- Pre-processors
- Cross-platform support! (Linux & Windows)

Snort has three main use models;

- `Sniffer Mode` - Read IP packets and prompt them in the console application.
- `Packet Logger Mode` - Log all IP packets (inbound and outbound) that visit the network.
- `NIDS` (`Network Intrusion Detection System`)  and NIPS (Network Intrusion Prevention System) Modes - Log/drop the packets that are deemed as malicious according to the user-defined rules.

---

## Task 4  First Interaction with Snort

### The First Interaction with Snort

First, let's verify snort is installed. The following command will show you the instance version.

```cmd
# version check
user@ubuntu$ snort -V

   ,,_     -*> Snort! <*-
  o"  )~   Version 2.9.7.0 GRE (Build XXXXXX) 
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team
           Copyright (C) 2014 Cisco and/or its affiliates. All rights reserved.
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.
           Using libpcap version 1.9.1 (with TPACKET_V3)
           Using PCRE version: 8.39 2016-06-14
           Using ZLIB version: 1.2.11
```
**Before getting your hands dirty, we should ensure our configuration file is valid.**

Here "-T" is used for testing configuration, and "-c" is identifying the configuration file (snort.conf).
Note that it is possible to use an additional configuration file by pointing it with "-c". 

```cmd
configuration check
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -T 

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
... [Output truncated]
        --== Initialization Complete ==--

   ,,_     -*> Snort! <*-
  o"  )~   Version 2.9.7.0 GRE (Build XXXX) 
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team
           Copyright (C) 2014 Cisco and/or its affiliates. All rights reserved.
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.
           Using libpcap version 1.9.1 (with TPACKET_V3)
           Using PCRE version: 8.39 2016-06-14
           Using ZLIB version: 1.2.11

           Rules Engine: SF_SNORT_DETECTION_ENGINE  Version 2.4  
           Preprocessor Object: SF_GTP  Version 1.1  
           Preprocessor Object: SF_SIP  Version 1.1  
           Preprocessor Object: SF_SSH  Version 1.1  
           Preprocessor Object: SF_SMTP  Version 1.1  
           Preprocessor Object: SF_POP  Version 1.0  
           Preprocessor Object: SF_DCERPC2  Version 1.0  
           Preprocessor Object: SF_IMAP  Version 1.0  
           Preprocessor Object: SF_DNP3  Version 1.1  
           Preprocessor Object: SF_SSLPP  Version 1.1  
           Preprocessor Object: SF_MODBUS  Version 1.1  
           Preprocessor Object: SF_SDF  Version 1.1  
           Preprocessor Object: SF_REPUTATION  Version 1.1  
           Preprocessor Object: SF_DNS  Version 1.1  
           Preprocessor Object: SF_FTPTELNET  Version 1.2  
... [Output truncated]
Snort successfully validated the configuration!
Snort exiting
```

Once we use a configuration file, snort got much more power! The configuration file is an all-in-one management file of the snort. Rules, plugins, detection mechanisms, default actions and output settings are identified here. It is possible to have multiple configuration files for different purposes and cases but can only use one at runtime.

Note that every time you start the Snort, it will automatically show the default banner and initial information about your setup. You can prevent this by using the "-q" parameter.

| Parameter | Description |
|:---:|:---:|
| -V / --version | This parameter provides information about your instance version. |
| -c | Identifying the configuration file |
| -T | Snort's self-test parameter, you can test your setup with this parameter. |
| -q | Quiet mode prevents snort from displaying the default banner and initial information about your setup. |

That was an easy one; let's continue exploring snort modes!

---

## Task 5  Operation Mode 1: Sniffer Mode

---

## Task 6  Operation Mode 2: Packet Logger Mode

---

## Task 7  Operation Mode 3: IDS/IPS

---

## Task 8  Operation Mode 4: PCAP Investigation

---

## Task 9  Snort Rule Structure

---

## Task 10  Snort2 Operation Logic: Points to Remember

---

## Task 11  Conclusion


---
---

- [SNORTOLOGY 101 - THE ANATOMY OF A SNORT RULE](https://snort-org-site.s3.amazonaws.com/production/document_files/files/000/000/116/original/Snort_rule_infographic.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAU7AK5ITMJQBJPARJ%2F20221114%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20221114T140032Z&X-Amz-Expires=172800&X-Amz-SignedHeaders=host&X-Amz-Signature=fda964fbf1b18a907a8e4d8082da10336c2aec7bf8dfe9f67391283bb08dc903)
