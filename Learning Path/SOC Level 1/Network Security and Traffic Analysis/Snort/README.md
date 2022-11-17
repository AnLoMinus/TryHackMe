![image](https://user-images.githubusercontent.com/51442719/201674330-21fe17e5-852f-4bdf-924f-28a0f98e2ac2.png)

# [Snort](https://tryhackme.com/room/snort)
### Learn how to use Snort to detect real-time threats, analyse recorded traffic files and identify anomalies.

---

- [Task 1  Introduction](#task-1--introduction)
- [Task 2  Interactive Material and VM](#task-2--interactive-material-and-vm)
- [Task 3  Introduction to IDS/IPS](#task-3--introduction-to-idsips)
- [Task 4  First Interaction with Snort](#task-4--first-interaction-with-snort)
- [Task 5  Operation Mode 1: Sniffer Mode](#task-5--operation-mode-1-sniffer-mode)
- [Task 6  Operation Mode 2: Packet Logger Mode](#task-6--operation-mode-2-packet-logger-mode)
- [Task 7  Operation Mode 3: IDS/IPS](#task-7--operation-mode-3-idsips)
- [Task 8  Operation Mode 4: PCAP Investigation](#task-8--operation-mode-4-pcap-investigation)
- [Task 9  Snort Rule Structure](#task-9--snort-rule-structure)
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

![image](https://user-images.githubusercontent.com/51442719/201778893-dc5b1002-5491-4199-a74d-778833c9f667.png)

### Let's run Snort in Sniffer Mode

Like tcpdump, Snort has various flags capable of viewing various data about the packet it is ingesting.

Sniffer mode parameters are explained in the table below;

| Parameter | Description |
|:---:|:---:|
| -v | Verbose. Display the TCP/IP output in the console. |
| -d | Display the packet data (payload). |
| -e | Display the link-layer (TCP/IP/UDP/ICMP) headers.  |
| -X | Display the full packet details in HEX. |
| -i | This parameter helps to define a specific network interface to listen/sniff. Once you have multiple interfaces, you can choose a specific interface to sniff.  |



Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action.

To do this, use the traffic-generator script (find this in the Task-Exercise folder)


### Sniffing with parameter "-i"

Start the Snort instance in verbose mode (-v) and use the interface (-i) "eth0"; `sudo snort -v-i eth0`

In case you have only one interface, Snort uses it by default. The above example demonstrates to sniff on the interface named "eth0". Once you simulate the parameter -v, you will notice it will automatically use the "eth0" interface and prompt it.

### Sniffing with parameter "-v"

Start the Snort instance in verbose mode (-v); `sudo snort -v`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start showing the  packets in verbosity mode as follows;

```cmd
# sniffing with -v
user@ubuntu$ sudo snort -v
                             
Running in packet dump mode

        --== Initializing Snort ==--
...
Commencing packet processing (pid=64)
12/01-20:10:13.846653 192.168.175.129:34316 -> 192.168.175.2:53
UDP TTL:64 TOS:0x0 ID:23826 IpLen:20 DgmLen:64 DF
Len: 36
=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+

12/01-20:10:13.846794 192.168.175.129:38655 -> 192.168.175.2:53
UDP TTL:64 TOS:0x0 ID:23827 IpLen:20 DgmLen:64 DF
Len: 36
===============================================================================
Snort exiting
```

As you can see in the given output, verbosity mode provides tcpdump like output information. Once we interrupt the sniffing with CTRL+C, it stops and summarises the sniffed packets.

### Sniffing with parameter "-d"

Start the Snort instance in dumping packet data mode (-d); sudo snort -d

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start showing the  packets in verbosity mode as follows;

```cmd
# sniffing with -d
user@ubuntu$ sudo snort -d
                             
Running in packet dump mode

        --== Initializing Snort ==--
...
Commencing packet processing (pid=67)

12/01-20:45:42.068675 192.168.175.129:37820 -> 192.168.175.2:53
UDP TTL:64 TOS:0x0 ID:53099 IpLen:20 DgmLen:56 DF
Len: 28
99 A5 01 00 00 01 00 00 00 00 00 00 06 67 6F 6F  .............goo
67 6C 65 03 63 6F 6D 00 00 1C 00 01              gle.com.....

=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+

WARNING: No preprocessors configured for policy 0.
12/01-20:45:42.070742 192.168.175.2:53 -> 192.168.175.129:44947
UDP TTL:128 TOS:0x0 ID:63307 IpLen:20 DgmLen:72
Len: 44
FE 64 81 80 00 01 00 01 00 00 00 00 06 67 6F 6F  .d...........goo
67 6C 65 03 63 6F 6D 00 00 01 00 01 C0 0C 00 01  gle.com.........
00 01 00 00 00 05 00 04 D8 3A CE CE              .........:..

=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
```

As you can see in the given output, packet data payload mode covers the verbose mode and provides more data.

### Sniffing with parameter "-de"

Start the Snort instance in dump (-d) and link-layer header grabbing (-e) mode; `snort -d -e`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start showing the  packets in verbosity mode as follows;

```cmd
# sniffing with -de
user@ubuntu$ sudo snort -de
                             
Running in packet dump mode

        --== Initializing Snort ==--
...
Commencing packet processing (pid=70)
12/01-20:55:26.958773 00:0C:29:A5:B7:A2 -> 00:50:56:E1:9B:9D type:0x800 len:0x46
192.168.175.129:47395 -> 192.168.175.2:53 UDP TTL:64 TOS:0x0 ID:64294 IpLen:20 DgmLen:56 DF
Len: 28
6D 9C 01 00 00 01 00 00 00 00 00 00 06 67 6F 6F  m............goo
67 6C 65 03 63 6F 6D 00 00 01 00 01              gle.com.....

=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+

WARNING: No preprocessors configured for policy 0.
12/01-20:55:26.965226 00:50:56:E1:9B:9D -> 00:0C:29:A5:B7:A2 type:0x800 len:0x56
192.168.175.2:53 -> 192.168.175.129:47395 UDP TTL:128 TOS:0x0 ID:63346 IpLen:20 DgmLen:72
Len: 44
6D 9C 81 80 00 01 00 01 00 00 00 00 06 67 6F 6F  m............goo
67 6C 65 03 63 6F 6D 00 00 01 00 01 C0 0C 00 01  gle.com.........
00 01 00 00 00 05 00 04 D8 3A D6 8E              .........:..
```

### Sniffing with parameter "-X"

Start the Snort instance in full packet dump mode (-X); sudo snort -X

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start showing the  packets in verbosity mode as follows;

```cmd
# sniffing with -X
user@ubuntu$ sudo snort -X
                             
Running in packet dump mode

        --== Initializing Snort ==--
...
Commencing packet processing (pid=76)
WARNING: No preprocessors configured for policy 0.
12/01-21:07:56.806121 192.168.175.1:58626 -> 239.255.255.250:1900
UDP TTL:1 TOS:0x0 ID:48861 IpLen:20 DgmLen:196
Len: 168
0x0000: 01 00 5E 7F FF FA 00 50 56 C0 00 08 08 00 45 00  ..^....PV.....E.
0x0010: 00 C4 BE DD 00 00 01 11 9A A7 C0 A8 AF 01 EF FF  ................
0x0020: FF FA E5 02 07 6C 00 B0 85 AE 4D 2D 53 45 41 52  .....l....M-SEAR
0x0030: 43 48 20 2A 20 48 54 54 50 2F 31 2E 31 0D 0A 48  CH * HTTP/1.1..H
0x0040: 4F 53 54 3A 20 32 33 39 2E 32 35 35 2E 32 35 35  OST: 239.255.255
0x0050: 2E 32 35 30 3A 31 39 30 30 0D 0A 4D 41 4E 3A 20  .250:1900..MAN: 
0x0060: 22 73 73 64 70 3A 64 69 73 63 6F 76 65 72 22 0D  "ssdp:discover".
0x0070: 0A 4D 58 3A 20 31 0D 0A 53 54 3A 20 75 72 6E 3A  .MX: 1..ST: urn:
0x0080: 64 69 61 6C 2D 6D 75 6C 74 69 73 63 72 65 65 6E  dial-multiscreen
0x0090: 2D 6F 72 67 3A 73 65 72 76 69 63 65 3A 64 69 61  -org:service:dia
0x00A0: 6C 3A 31 0D 0A 55 53 45 52 2D 41 47 45 4E 54 3A  l:1..USER-AGENT:
0x00B0: 20 43 68 72 6F 6D 69 75 6D 2F 39 35 2E 30 2E 34   Chromium/95.0.4
0x00C0: 36 33 38 2E 36 39 20 57 69 6E 64 6F 77 73 0D 0A  638.69 Windows..
0x00D0: 0D 0A                                            ..

=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+

WARNING: No preprocessors configured for policy 0.
12/01-21:07:57.624205 216.58.214.142 -> 192.168.175.129
ICMP TTL:128 TOS:0x0 ID:63394 IpLen:20 DgmLen:84
Type:0  Code:0  ID:15  Seq:1  ECHO REPLY
0x0000: 00 0C 29 A5 B7 A2 00 50 56 E1 9B 9D 08 00 45 00  ..)....PV.....E.
0x0010: 00 54 F7 A2 00 00 80 01 24 13 D8 3A D6 8E C0 A8  .T......$..:....
0x0020: AF 81 00 00 BE B6 00 0F 00 01 2D E4 A7 61 00 00  ..........-..a..
0x0030: 00 00 A4 20 09 00 00 00 00 00 10 11 12 13 14 15  ... ............
0x0040: 16 17 18 19 1A 1B 1C 1D 1E 1F 20 21 22 23 24 25  .......... !"#$%
0x0050: 26 27 28 29 2A 2B 2C 2D 2E 2F 30 31 32 33 34 35  &'()*+,-./012345
0x0060: 36 37                                            67

=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
```

Note that you can use the parameters both in combined and separated form as follows;

- `snort -v`
- `snort -vd`
- `snort -de`
- `snort -v -d -e`
- `snort -X`

Make sure you understand and practice each parameter with different types of traffic and discover your favourite combination.

---

## Task 6  Operation Mode 2: Packet Logger Mode

![image](https://user-images.githubusercontent.com/51442719/201781118-9bc9fbd6-2f19-4e05-8c0a-85ee6ff297a7.png)

### Let's run Snort in Logger Mode

You can use Snort as a sniffer and log the sniffed packets via logger mode. You only need to use the packet logger mode parameters, and Snort does the rest to accomplish this.

Packet logger parameters are explained in the table below;

| Parameter | Description |
|:---:|:---:|
| -l | Logger mode, target log and alert output directory. Default output folder is /var/log/snort The default action is to dump as tcpdump format in /var/log/snort |
| -K ASCII | Log packets in ASCII format. |
| -r | Reading option, read the dumped logs in Snort. |
| -n | Specify the number of packets that will process/read. Snort will stop after reading the specified number of packets. |

Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action.


### Logfile Ownership
Before generating logs and investigating them, we must remember the Linux file ownership and permissions. No need to deep dive into user types and permissions. The fundamental file ownership rule; whoever creates a file becomes the owner of the corresponding file.

Snort needs superuser (root) rights to sniff the traffic, so once you run the snort with the "sudo" command, the "root" account will own the generated log files. Therefore you will need "root" rights to investigate the log files. There are two different approaches to investigate the generated log files;

- Elevation of privileges - You can elevate your privileges to examine the files. You can use the "sudo" command to execute your command as a superuser with the following command `sudo command`. You can also elevate the session privileges and switch to the superuser account to examine the generated log files with the following command: `sudo su`

- Changing the ownership of files/directories - You can also change the ownership of the file/folder to read it as your user: `sudo chown username file` or `sudo chown username -R directory` The "-R" parameter helps recursively process the files and directories.

### Logging with parameter "-l"

First, start the Snort instance in packet logger mode; `sudo snort -dev -l` .

Now start ICMP/HTTP traffic with the traffic-generator script.

Once the traffic is generated, Snort will start showing the packets and log them in the target directory. You can configure the default output directory in snort.config file. However, you can use the "-l" parameter to set a target directory. Identifying the default log directory is useful for continuous monitoring operations, and the "`-l`" parameter is much more useful for testing purposes.

The `-l` . part of the command creates the logs in the current directory. You will need to use this option to have the logs for each exercise in their folder.

```cmd
# logging with -l
user@ubuntu$ sudo snort -dev -l .
                             
Running in packet logging mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Log directory = /var/log/snort
pcap DAQ configured to passive.
Acquiring network traffic from "ens33".
Decoding Ethernet

        --== Initialization Complete ==--
...
Commencing packet processing (pid=2679)
WARNING: No preprocessors configured for policy 0.
WARNING: No preprocessors configured for policy 0.
```

Now, let's check the generated log file. Note that the log file names will be different in your case.

```cmd
# checking the log file
user@ubuntu$ ls .
                             
snort.log.1638459842
```

As you can see, it is a single all-in-one log file. It is a binary/tcpdump format log. This is what it looks like in the folder view.

![image](https://user-images.githubusercontent.com/51442719/201788284-240378d5-cf6c-444e-a38e-717d4fa907b2.png)

### Logging with parameter "-K ASCII"

Start the Snort instance in packet logger mode; `sudo snort -dev -K ASCII`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, Snort will start showing the  packets in verbosity mode as follows;

```cmd
# logging with -K ASCII
user@ubuntu$ sudo snort -dev -K ASCII -l .
                             
Running in packet logging mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Log directory = /var/log/snort
pcap DAQ configured to passive.
Acquiring network traffic from "ens33".
Decoding Ethernet

        --== Initialization Complete ==--
...
Commencing packet processing (pid=2679)
WARNING: No preprocessors configured for policy 0.
WARNING: No preprocessors configured for policy 0.
```

Now, let's check the generated log file.

```cmd
# Checking the log file
user@ubuntu$ ls .
                             
142.250.187.110  192.168.175.129  snort.log.1638459842
```

This is what it looks like in the folder view.

![image](https://user-images.githubusercontent.com/51442719/201788457-cd93036c-9abf-4538-9a21-4b28ca626109.png)

The logs created with "-K ASCII" parameter is entirely different. There are two folders with IP address names. Let's look into them.

```cmd
# checking the log file
user@ubuntu$ ls ./192.168.175.129/
                             
ICMP_ECHO  UDP:36648-53  UDP:40757-53  UDP:47404-53  UDP:50624-123
```

Once we look closer at the created folders, we can see that the logs are in ASCII and categorised format, so it is possible to read them without using a Snort instance.

This is what it looks like in the folder view.

![image](https://user-images.githubusercontent.com/51442719/201788510-7987951c-af4c-4d98-b7ec-61f58e1161b5.png)


In a nutshell, ASCII mode provides multiple files in human-readable format, so it is possible to read the logs easily by using a text editor. By contrast with ASCII format, binary format is not human-readable and requires analysis using Snort or an application like tcpdump.

Let's compare the ASCII format with the binary format by opening both of them in a text editor. The difference between the binary log file and the ASCII log file is shown below. (Left side: binary format. Right side: ASCII format).

![image](https://user-images.githubusercontent.com/51442719/201788538-be3d54ea-004a-4009-8734-357fe4f10b04.png)


### Reading generated logs with parameter "-r"

Start the Snort instance in packet reader mode; `sudo snort -r`

```cmd
# reading log files with -r

user@ubuntu$ sudo snort -r snort.log.1638459842
                             
Running in packet dump mode

        --== Initializing Snort ==--
Initializing Output Plugins!
pcap DAQ configured to read-file.
Acquiring network traffic from "snort.log.1638459842".

        --== Initialization Complete ==--
...
Commencing packet processing (pid=3012)
WARNING: No preprocessors configured for policy 0.
12/02-07:44:03.123225 192.168.175.129 -> 142.250.187.110
ICMP TTL:64 TOS:0x0 ID:41900 IpLen:20 DgmLen:84 DF
Type:8  Code:0  ID:1   Seq:49  ECHO
=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
WARNING: No preprocessors configured for policy 0.
12/02-07:44:26.169620 192.168.175.129 -> 142.250.187.110
ICMP TTL:64 TOS:0x0 ID:44765 IpLen:20 DgmLen:84 DF
Type:8  Code:0  ID:1   Seq:72  ECHO
===============================================================================
Packet I/O Totals:
   Received:           51
   Analyzed:           51 (100.000%)
    Dropped:            0 (  0.000%)
   Filtered:            0 (  0.000%)
Outstanding:            0 (  0.000%)
   Injected:            0
===============================================================================
Breakdown by protocol (includes rebuilt packets):
...
      Total:           51
===============================================================================
Snort exiting
```

Note that Snort can read and handle the binary like output (tcpdump and Wireshark also can handle this log format). However, if you create logs with "-K ASCII" parameter, Snort will not read them. As you can see in the above output, Snort read and displayed the log file just like in the sniffer mode.

Opening log file with tcpdump.

```cmd
# Opening the log file with tcpdump
user@ubuntu$ sudo tcpdump -r snort.log.1638459842 -ntc 10
                             
reading from file snort.log.1638459842, link-type EN10MB (Ethernet)
IP 192.168.175.129 > 142.250.187.110: ICMP echo request, id 1, seq 49, length 64
IP 142.250.187.110 > 192.168.175.129: ICMP echo reply, id 1, seq 49, length 64
IP 192.168.175.129 > 142.250.187.110: ICMP echo request, id 1, seq 50, length 64
IP 142.250.187.110 > 192.168.175.129: ICMP echo reply, id 1, seq 50, length 64
IP 192.168.175.129 > 142.250.187.110: ICMP echo request, id 1, seq 51, length 64
IP 142.250.187.110 > 192.168.175.129: ICMP echo reply, id 1, seq 51, length 64
IP 192.168.175.129 > 142.250.187.110: ICMP echo request, id 1, seq 52, length 64
IP 142.250.187.110 > 192.168.175.129: ICMP echo reply, id 1, seq 52, length 64
IP 192.168.175.1.63096 > 239.255.255.250.1900: UDP, length 173
IP 192.168.175.129 > 142.250.187.110: ICMP echo request, id 1, seq 53, length 64
```

Opening log file with Wireshark.

![image](https://user-images.githubusercontent.com/51442719/201788676-43bb1415-6125-425a-8ad3-583c002b6f69.png)

"-r" parameter also allows users to filter the binary log files. You can filter the processed log to see specific packets with the "-r" parameter and Berkeley Packet Filters (BPF). 

- `sudo snort -r logname.log -X`
- `sudo snort -r logname.log icmp`
- `sudo snort -r logname.log tcp`
- `sudo snort -r logname.log 'udp and port 53'`

The output will be the same as the above, but only packets with the chosen protocol will be shown. Additionally, you can specify the number of processes with the parameter "-n". The following command will process only the first 10 packets:

`snort -dvr logname.log -n 10`

Please use the following resources to understand how the BPF works and its use.

- https://en.wikipedia.org/wiki/Berkeley_Packet_Filter
- https://biot.com/capstats/bpf.html
- https://www.tcpdump.org/manpages/tcpdump.1.html

Now, use the attached VM and navigate to the Task-Exercises/Exercise-Files/TASK-6 folder to answer the questions!

---

## Task 7  Operation Mode 3: IDS/IPS

![image](https://user-images.githubusercontent.com/51442719/201790226-4cb2410b-23bf-42b0-9ea1-31c633c72df7.png)

### Snort in IDS/IPS Mode

Capabilities of Snort are not limited to sniffing and logging the traffic. IDS/IPS mode helps you manage the traffic according to user-defined rules.

Note that (N)IDS/IPS mode depends on the rules and configuration. TASK-10 summarises the essential paths, files and variables. Also, TASK-3 covers configuration testing. Here, we need to understand the operating logic first, and then we will be going into rules in TASK-9.

### Let's run Snort in IDS/IPS Mode

NIDS mode parameters are explained in the table below;

| Parameter | Description |
|:---:|:---:|
| -c | Defining the configuration file. |
| -T | Testing the configuration file. |
| -N | Disable logging. |
| -D | Background mode. |
| -A | Alert modes;  full: Full alert mode, providing all possible information about the alert. This one also is the default mode; once you use -A and don't specify any mode, snort uses this mode.  fast:  Fast mode shows the alert message, timestamp, source and destination IP, along with port numbers. console: Provides fast style alerts on the console screen. cmg: CMG style, basic header details with payload in hex and text format. none: Disabling alerting. |


Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action. To do this, use the traffic-generator script and sniff the traffic. 

Once you start running IDS/IPS mode, you need to use rules. As we mentioned earlier, we will use a pre-defined ICMP rule as an example. The defined rule will only generate alerts in any direction of ICMP packet activity.

`alert icmp any any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)`

This rule is located in "/etc/snort/rules/local.rules".

Remember, in this module, we will focus only on the operating modes. The rules are covered in TASK9&10. Snort will create an "alert" file if the traffic flow triggers an alert. One last note; once you start running IPS/IDS mode, the sniffing and logging mode will be semi-passive. However, you can activate the functions using the parameters discussed in previous tasks. (-i, -v, -d, -e, -X, -l, -K ASCII) If you don't remember the purpose of these commands, please revisit TASK4.

### IDS/IPS mode with parameter "-c and -T"

Start the Snort instance and test the configuration file. `sudo snort -c /etc/snort/snort.conf -T`  This command will check your configuration file and prompt it if there is any misconfiguratioın in your current setting. You should be familiar with this command if you covered TASK3. If you don't remember the output of this command, please revisit TASK4.

### IDS/IPS mode with parameter "-N"

Start the Snort instance and disable logging by running the following command: `sudo snort -c /etc/snort/snort.conf -N`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. This command will disable logging mode. The rest of the other functions will still be available (if activated).

The command-line output will provide the information requested with the parameters. So, if you activate verbosity (-v) or full packet dump (-X) you will still have the output in the console, but there will be no logs in the log folder.


### IDS/IPS mode with parameter "-D"

Start the Snort instance in background mode with the following command: `sudo snort -c /etc/snort/snort.conf -D`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start processing the packets and accomplish the given task with additional parameters.

```cmd
# running in background mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -D

Spawning daemon child...
My daemon child 2898 lives...
Daemon parent exiting (0)
```

The command-line output will provide the information requested with the parameters. So, if you activate verbosity (-v) or full packet dump (-X) with packet logger mode (-l) you will still have the logs in the logs folder, but there will be no output in the console.
Once you start the background mode and want to check the corresponding process, you can easily use the "ps" command as shown below;

```cmd
# running in background mode
user@ubuntu$ ps -ef | grep snort

root        2898    1706  0 05:53 ?        00:00:00 snort -c /etc/snort/snort.conf -D
```

If you want to stop the daemon, you can easily use the "kill" command to stop the process.

```cmd
# running in background mode
user@ubuntu$ sudo kill -9 2898
```

Note that daemon mode is mainly used to automate the Snort. This parameter is mainly used in scripts to start the Snort service in the background. It is not recommended to use this mode unless you have a working knowledge of Snort and stable configuration.

### IDS/IPS mode with parameter "-A"

Remember that there are several alert modes available in snort;

- console: Provides fast style alerts on the console screen.
- cmg: Provides basic header details with payload in hex and text format.
- full: Full alert mode, providing all possible information about the alert.
- fast: Fast mode, shows the alert message, timestamp, source and destination ıp along with port numbers.
- none: Disabling alerting.

In this section, only the "console" and "cmg" parameters provide alert information in the console. It is impossible to identify the difference between the rest of the alert modes via terminal. Differences can be identified by looking at generated logs. 

At the end of this section, we will compare the "full", "fast" and "none" modes. Remember that these parameters don't provide console output, so we will continue to identify the differences through log formats.

### IDS/IPS mode with parameter "-A console"

Console mode provides fast style alerts on the console screen. Start the Snort instance in console alert mode (-A console ) with the following command `sudo snort -c /etc/snort/snort.conf -A console`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

```cmd
running in console alert mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -A console
Running in IDS mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
Parsing Rules file "/etc/snort/snort.conf"
...
Commencing packet processing (pid=3743)
12/12-02:08:27.577495  [**] [1:366:7] ICMP PING *NIX [**] [Classification: Misc activity] [Priority: 3] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-02:08:27.577495  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-02:08:27.577495  [**] [1:384:5] ICMP PING [**] [Classification: Misc activity] [Priority: 3] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-02:08:27.609719  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
^C*** Caught Int-Signal
12/12-02:08:29.595898  [**] [1:366:7] ICMP PING *NIX [**] [Classification: Misc activity] [Priority: 3] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-02:08:29.595898  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-02:08:29.595898  [**] [1:384:5] ICMP PING [**] [Classification: Misc activity] [Priority: 3] {ICMP} 192.168.175.129 -> 142.250.187.110
===============================================================================
Run time for packet processing was 26.25844 seconds
Snort processed 88 packets.
```

### IDS/IPS mode with parameter "-A cmg"

Cmg mode provides basic header details with payload in hex and text format. Start the Snort instance in cmg alert mode (-A cmg ) with the following command `sudo snort -c /etc/snort/snort.conf -A cmg`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

```cmd
running in cmg alert mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -A cmg
Running in IDS mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
Parsing Rules file "/etc/snort/snort.conf"
...
Commencing packet processing (pid=3743)
12/12-02:23:56.944351  [**] [1:366:7] ICMP PING *NIX [**] [Classification: Misc activity] [Priority: 3] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-02:23:56.944351 00:0C:29:A5:B7:A2 -> 00:50:56:E1:9B:9D type:0x800 len:0x62
192.168.175.129 -> 142.250.187.110 ICMP TTL:64 TOS:0x0 ID:10393 IpLen:20 DgmLen:84 DF
Type:8  Code:0  ID:4   Seq:1  ECHO
BC CD B5 61 00 00 00 00 CE 68 0E 00 00 00 00 00  ...a.....h......
10 11 12 13 14 15 16 17 18 19 1A 1B 1C 1D 1E 1F  ................
20 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F   !"#$%&'()*+,-./
30 31 32 33 34 35 36 37                          01234567

=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
```

Let's compare the console and cmg outputs before moving on to other alarm types. As you can see in the given outputs above, console mode provides basic header and rule information. Cmg mode provides full packet details along with rule information. 


### IDS/IPS mode with parameter "-A fast"

Fast mode provides alert messages, timestamps, and source and destination IP addresses. Remember, there is no console output in this mode. Start the Snort instance in fast alert mode (-A fast ) with the following command `sudo snort -c /etc/snort/snort.conf -A fast`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

```cmd
running in fast alert mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -A fast
Running in IDS mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
Parsing Rules file "/etc/snort/snort.conf"
...
Commencing packet processing (pid=3743)
=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
```

Let's check the alarm file;

![image](https://user-images.githubusercontent.com/51442719/201791817-e6010c2b-6f4c-463a-b524-b1e43ba3e3aa.png)

As you can see in the given picture above, fast style alerts contain summary information on the action like direction and alert header.

### IDS/IPS mode with parameter "-A full"

Full alert mode provides all possible information about the alert. Remember, there is no console output in this mode. Start the Snort instance in full alert mode (-A full ) with the following command `sudo snort -c /etc/snort/snort.conf -A full`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

```cmd
running in full alert mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -A full
Running in IDS mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
Parsing Rules file "/etc/snort/snort.conf"
...
Commencing packet processing (pid=3744)
=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
```

Let's check the alarm file;

![image](https://user-images.githubusercontent.com/51442719/201791976-28a7de37-9d53-4fe3-9133-ad58103311b7.png)

 As you can see in the given picture above, full style alerts contain all possible information on the action.

### IDS/IPS mode with parameter "-A none"

Disable alerting. This mode doesn't create the alert file. However, it still logs the traffic and creates a log file in binary dump format. Remember, there is no console output in this mode. Start the Snort instance in none alert mode (-A none) with the following command `sudo snort -c /etc/snort/snort.conf -A none`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file. 

```cmd
running in none alert mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -A none
Running in IDS mode

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
Parsing Rules file "/etc/snort/snort.conf"
...
Commencing packet processing (pid=3745)
=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+
```

As you can see in the picture below, there is no alert file. Snort only generated the log file.

![image](https://user-images.githubusercontent.com/51442719/201792086-5d9ccbf6-0cbb-400f-b067-b0cbe4e36555.png)

### IDS/IPS mode: "Using rule file without configuration file"

It is possible to run the Snort only with rules without a configuration file. Running the Snort in this mode will help you test the user-created rules. However, this mode will provide less performance.

```cmd
running without configuration file
user@ubuntu$ sudo snort -c /etc/snort/rules/local.rules -A console
Running in IDS mode

12/12-12:13:29.167955  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:29.200543  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:30.169785  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:30.201470  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:31.172101  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
^C*** Caught Int-Signal
```

### IPS mode and dropping packets

Snort IPS mode activated with -Q --daq afpacket parameters. You can also activate this mode by editing snort.conf file. However, you don't need to edit snort.conf file in the scope of this room. Review the bonus task or snort manual for further information on daq and advanced configuration settings: `-Q --daq afpacket`

Activate the Data Acquisition (DAQ) modules and use the afpacket module to use snort as an IPS: -`i eth0:eth1`

Identifying interfaces note that Snort IPS require at least two interfaces to work. Now run the traffic-generator script as sudo and start ICMP/HTTP traffic.

```cmd
running IPS mode
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console
Running in IPS mode

12/18-07:40:01.527100  [Drop] [**] [1:1000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.131 -> 192.168.175.2
12/18-07:40:01.552811  [Drop] [**] [1:1000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 172.217.169.142 -> 192.168.1.18
12/18-07:40:01.566232  [Drop] [**] [1:1000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.131 -> 192.168.175.2
12/18-07:40:02.517903  [Drop] [**] [1:1000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.1.18 -> 172.217.169.142
12/18-07:40:02.550844  [Drop] [**] [1:1000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 172.217.169.142 -> 192.168.1.18
^C*** Caught Int-Signal
```

As you can see in the picture above, Snort blocked the packets this time. We used the same rule with a different action (drop/reject). Remember, for the scope of this task; our point is the operating mode, not the rule.


### Investigate the traffic with the default configuration file.

- `sudo snort -c /etc/snort/snort.conf -A full -l .`

Execute the traffic generator script and choose "TASK-7 Exercise". Wait until the traffic stops, then stop the Snort instance. Now analyse the output summary and answer the question.


---

## Task 8  Operation Mode 4: PCAP Investigation

![image](https://user-images.githubusercontent.com/51442719/201798915-6ad88628-5ccf-4a0f-85ca-f42db0f62839.png)

### Let's investigate PCAPs with Snort

Capabilities of Snort are not limited to sniffing, logging and detecting/preventing the threats. PCAP read/investigate mode helps you work with pcap files. Once you have a pcap file and process it with Snort, you will receive default traffic statistics with alerts depending on your ruleset.

Reading a pcap without using any additional parameters we discussed before will only overview the packets and provide statistics about the file. In most cases, this is not very handy. We are investigating the pcap with Snort to benefit from the rules and speed up our investigation process by using the known patterns of threats. 

Note that we are pretty close to starting to create rules. Therefore, you need to grasp the working mechanism of the Snort, learn the discussed parameters and begin combining the parameters for different purposes.

PCAP mode parameters are explained in the table below;

| Parameter | Description |
|:---:|:---:|
| -r / --pcap-single= | Read a single pcap |
| --pcap-list="" | Read pcaps provided in command (space separated). |
| --pcap-show | Show pcap name on console during processing. |

### Investigating single PCAP with parameter "-r"

For test purposes, you can still test the default reading option with pcap by using the following command `snort -r icmp-test.pcap`

Let's investigate the pcap with our configuration file and see what will happen. `sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10`

If you don't remember the purpose of the parameters in the given command, please revisit previous tasks and come back again!

```cmd
investigating single pcap file
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10

12/12-12:13:29.167955  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:29.200543  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:30.169785  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:30.201470  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:31.172101  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:31.204104  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:32.174106  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:32.208683  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:33.176920  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:33.208359  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
```

Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic and prompted the alerts according to our ruleset.


### Investigating multiple PCAPs with parameter "--pcap-list"

Let's investigate multiple pcaps with our configuration file and see what will happen. 

- `sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console -n 10`

```cmd
investigating multiple pcap files
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console

12/12-12:13:29.167955  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:29.200543  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:30.169785  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:30.201470  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:31.172101  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
...
12/12-12:13:31.204104  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:32.174106  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:32.208683  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:33.176920  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:33.208359  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
```

Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic and prompted the alerts according to our ruleset.

Here is one point to notice: we've processed two pcaps, and there are lots of alerts, so it is impossible to match the alerts with provided pcaps without snort's help. We need to separate the pcap process to identify the source of the alerts.


### Investigating multiple PCAPs with parameter "--pcap-show"

Let's investigate multiple pcaps, distinguish each one, and see what will happen. 

- `sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console --pcap-show`

```cmd
investigating multiple pcap files wth pcap info
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console --pcap-show 

Reading network traffic from "icmp-test.pcap" with snaplen = 1514
12/12-12:13:29.167955  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:29.200543  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:30.169785  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
...

Reading network traffic from "http2.pcap" with snaplen = 1514
12/12-12:13:35.213176  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
12/12-12:13:36.182950  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 192.168.175.129 -> 142.250.187.110
12/12-12:13:38.223470  [**] [1:10000001:0] ICMP Packet found [**] [Priority: 0] {ICMP} 142.250.187.110 -> 192.168.175.129
...
```

Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic, distinguished each pcap file and prompted the alerts according to our ruleset.
Now, use the attached VM and navigate to the Task-Exercises/Exercise-Files/TASK-8 folder to answer the questions!


---

## Task 9  Snort Rule Structure

![image](https://user-images.githubusercontent.com/51442719/201801029-3cc1213c-7c1f-4366-be4b-07ebe505fd2f.png)

### Let's Learn Snort Rules!

Understanding the Snort rule format is essential for any blue and purple teamer.  The primary structure of the snort rule is shown below;

![image](https://user-images.githubusercontent.com/51442719/201801059-e385be46-a52f-4853-92b1-4bff4d03386e.png)

Each rule should have a type of action, protocol, source and destination IP, source and destination port and an option. Remember, Snort is in passive mode by default. So most of the time, you will use Snort as an IDS. You will need to start "inline mode" to turn on IPS mode. But before you start playing with inline mode, you should be familiar with Snort features and rules.

The Snort rule structure is easy to understand but difficult to produce. You should be familiar with rule options and related details to create efficient rules. It is recommended to practice Snort rules and option details for different use cases.

We will cover the basic rule structure in this room and help you take a step into snort rules. You can always advance your rule creation skills with different rule options by practising different use cases and studying rule option details in depth. We will focus on two actions; "alert"  for IDS mode and "reject" for IPS mode.

Rules cannot be processed without a header. Rule options are "optional" parts. However, it is almost impossible to detect sophisticated attacks without using the rule options.

| Action | There are several actions for rules. Make sure you understand the functionality and test it before creating rules for live systems. The most common actions are listed below. `alert`: Generate an alert and log the packet. `log`: Log the packet. `drop`: Block and log the packet. `reject`: Block the packet, log it and terminate the packet session.  |
|:---:|---|
| Protocol | Protocol parameter identifies the type of the protocol that filtered for the rule. Note that Snort2 supports only four protocols filters in the rules (IP, TCP, UDP and ICMP). However, you can detect the application flows using port numbers and options. For instance, if you want to detect FTP traffic, you cannot use the FTP keyword in the protocol field but filter the FTP traffic by investigating TCP traffic on port 21. |

### IP and Port Numbers

These parameters identify the source and destination IP addresses and associated port numbers filtered for the rule.

| IP Filtering | alert icmp 192.168.1.56 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each ICMP packet originating from the 192.168.1.56 IP address. |
|:---:|---|
| Filter an IP range | alert icmp 192.168.1.0/24 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each ICMP packet originating from the 192.168.1.0/24 subnet. |
| Filter multiple IP ranges | alert icmp [192.168.1.0/24, 10.1.1.0/24] any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each ICMP packet originating from the 192.168.1.0/24 and 10.1.1.0/24 subnets. |
| Exclude IP addresses/ranges | "negation operator" is used for excluding specific addresses and ports. Negation operator is indicated with "!" alert icmp !192.168.1.0/24 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each ICMP packet not originating from the 192.168.1.0/24 subnet. |
| Port Filtering | alert tcp !192.168.1.0/24 21 <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each TCP packet originating from port 21. |
| Exclude a specific port | alert tcp !192.168.1.0/24 !21 <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each TCP packet not originating from port 21. |
| Filter a port range (Type 1) | alert tcp !192.168.1.0/24 1:1024 <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each TCP packet originating from ports between 1-1024. |
| Filter a port range (Type 2) | alert icmp any :1024 <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each TCP packet originating from ports less than or equal to 1024. |
| Filter a port range (Type 3) | alert icmp any 1024: <> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each TCP packet originating from a source port higher than or equal to 1024. |
| Filter a port range (Type 4) | alert icmp any 80,1024: <> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;) This rule will create alerts for each TCP packet originating from a source port 80 and higher than or equal to 1024. |

### Direction

The direction operator indicates the traffic flow to be filtered by Snort. The left side of the rule shows the source, and the right side shows the destination.

- -> Source to destination flow.
- <> Bidirectional flow

> Note that there is no "<-" operator in Snort.

![image](https://user-images.githubusercontent.com/51442719/201801763-5052a6ea-1c8e-4b1f-8312-db66022516f8.png)


### There are three main rule options in Snort;

- `General Rule Options` - Fundamental rule options for Snort. 
- `Payload Rule Options` - Rule options that help to investigate the payload data. These options are helpful to detect specific payload patterns.
- `Non-Payload Rule Options` - Rule options that focus on non-payload data. These options will help create specific patterns and identify network issues.


### General Rule Options

| Msg | The message field is a basic prompt and quick identifier of the rule. Once the rule is triggered, the message filed will appear in the console or log. Usually, the message part is a one-liner that summarises the event. |
|:---:|---|
| Sid | Snort rule IDs (SID) come with a pre-defined scope, and each rule must have a SID in a proper format. There are three different scopes for SIDs shown below. <100: Reserved rules 100-999,999: Rules came with the build. >=1,000,000: Rules created by user. Briefly, the rules we will create should have sid greater than 100.000.000. Another important point is; SIDs should not overlap, and each id must be unique.  |
| Reference | Each rule can have additional information or reference to explain the purpose of the rule or threat pattern. That could be a Common Vulnerabilities and Exposures (CVE) id or external information. Having references for the rules will always help analysts during the alert and incident investigation. |
| Rev | Snort rules can be modified and updated for performance and efficiency issues. Rev option help analysts to have the revision information of each rule. Therefore, it will be easy to understand rule improvements. Each rule has its unique rev number, and there is no auto-backup feature on the rule history. Analysts should keep the rule history themselves. Rev option is only an indicator of how many times the rule had revisions. alert icmp any any <> any any (msg: "ICMP Packet Found"; sid: 100001; reference:cve,CVE-XXXX; rev:1;) |

### Payload Detection Rule Options

| Content | Payload data. It matches specific payload data by ASCII, HEX or both. It is possible to use this option multiple times in a single rule. However, the more you create specific pattern match features, the more it takes time to investigate a packet. Following rules will create an alert for each HTTP packet containing the keyword "GET". This rule option is case sensitive! ASCII mode - alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; sid: 100001; rev:1;) HEX mode - alert tcp any any <> any 80  (msg: "GET Request Found"; content:"\|47 45 54\|"; sid: 100001; rev:1;) |
|:---:|---|
| Nocase | Disabling case sensitivity. Used for enhancing the content searches. alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; nocase; sid: 100001; rev:1;) |
| Fast_pattern | Prioritise content search to speed up the payload search operation. By default, Snort uses the biggest content and evaluates it against the rules. "fast_pattern" option helps you select the initial packet match with the specific value for further investigation. This option always works case insensitive and can be used once per rule. Note that this option is required when using multiple "content" options.  The following rule has two content options, and the fast_pattern option tells to snort to use the first content option (in this case, "GET") for the initial packet match.  alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; fast_pattern; content:"www";  sid:100001; rev:1;) |

### Non-Payload Detection Rule Options

There are rule options that focus on non-payload data. These options will help create specific patterns and identify network issues.

| ID | Filtering the IP id field. alert tcp any any <> any any (msg: "ID TEST"; id:123456; sid: 100001; rev:1;) |
|:---:|---|
| Flags | Filtering the TCP flags. F - FIN S - SYN R - RST P - PSH A - ACK U - URG  alert tcp any any <> any any (msg: "FLAG TEST"; flags:S;  sid: 100001; rev:1;) |
| Dsize | Filtering the packet payload size. dsize:min<>max; dsize:>100 dsize:<100 alert ip any any <> any any (msg: "SEQ TEST"; dsize:100<>300;  sid: 100001; rev:1;) |
| Sameip | Filtering the source and destination IP addresses for duplication. alert ip any any <> any any (msg: "SAME-IP TEST";  sameip; sid: 100001; rev:1;) |

Remember, once you create a rule, it is a local rule and should be in your "local.rules" file. This file is located under "/etc/snort/rules/local.rules". A quick reminder on how to edit your local rules is shown below.

```cmd
modifying the local rules
user@ubuntu$ sudo gedit /etc/snort/rules/local.rules 
```

That is your "local.rules" file.

![image](https://user-images.githubusercontent.com/51442719/201802059-bcbc7faf-fe9b-477b-9b50-50c20b5e6164.png)

Note that there are some default rules activated with snort instance. These rules are deactivated to manage your rules and improve your exercise experience. For further information, please refer to the TASK-10 or [Snort manual](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/).

By this point, we covered the primary structure of the Snort rules. Understanding and practicing the fundamentals is suggested before creating advanced rules and using additional options.

Wow! We have covered the fundamentals of the Snort rules!   Now, use the attached VM and navigate to the Task-Exercises/Exercise-Files/TASK-9 folder to answer the questions! Note that you can use the following command to create the logs in the current directory: `-l .`


---

## Task 10  Snort2 Operation Logic: Points to Remember

### Points to Remember

Main Components of Snort

- `Packet Decoder` - Packet collector component of Snort. It collects and prepares the packets for pre-processing. 
- `Pre-processors` - A component that arranges and modifies the packets for the detection engine.
- `Detection Engine` - The primary component that process, dissect and analyse the packets by applying the rules. 
- `Logging and Alerting` - Log and alert generation component.
- `Outputs and Plugins` - Output integration modules (i.e. alerts to syslog/mysql) and additional plugin (rule management detection plugins) support is done with this component.

### There are three types of rules available for snort

- `Community Rules` - Free ruleset under the GPLv2. Publicly accessible, no need for registration.
- `Registered Rules` - Free ruleset (requires registration). This ruleset contains subscriber rules with 30 days delay.
- `Subscriber Rules` (Paid) - Paid ruleset (requires subscription). This ruleset is the main ruleset and is updated twice a week (Tuesdays and Thursdays).

You can download and read more on the rules [here](https://www.snort.org/downloads).

> `Note`: Once you install Snort2, it automatically creates the required directories and files. However, if you want to use the community or the paid rules, you need to indicate each rule in the snort.conf file.

Since it is a long, all-in-one configuration file, editing it without causing misconfiguration is troublesome for some users. That is why Snort has several rule updating modules and integration tools. To sum up, never replace your configured Snort configuration files; you must edit your configuration files manually or update your rules with additional tools and modules to not face any fail/crash or lack of feature.

- `snort.conf`: Main configuration file.
- `local.rules`: User-generated rules file.

Let's start with overviewing the main configuration file (snort.conf) `sudo gedit /etc/snort/snort.conf`

**Navigate to the "Step #1: Set the network variables." section.**

This section manages the scope of the detection and rule paths.

| TAG NAME | INFO | EXAMPLE |
|:---:|:---:|:---:|
| HOME_NET | That is where we are protecting. |  'any' OR '192.168.1.1/24' |
| EXTERNAL_NET  | This field is the external network, so we need to keep it as 'any' or '!$HOME_NET'. | 'any' OR '!$HOME_NET' |
| RULE_PATH | Hardcoded rule path. | /etc/snort/rules |
| SO_RULE_PATH | These rules come with registered and subscriber rules. | $RULE_PATH/so_rules |
| PREPROC_RULE_PATH | These rules come with registered and subscriber rules. | $RULE_PATH/plugin_rules |

**Navigate to the "Step #2: Configure the decoder." section.**

In this section, you manage the IPS mode of snort. The single-node installation model IPS model works best with "afpacket" mode. You can enable this mode and run Snort in IPS.

| TAG NAME | INFO | EXAMPLE |
|:---:|:---:|:---:|
| #config daq: | IPS mode selection. | afpacket |
| #config daq_mode: | Activating the inline mode | inline |
| #config logdir: | Hardcoded default log path. | /var/logs/snort |

Data Acquisition Modules (DAQ) are specific libraries used for packet I/O, bringing flexibility to process packets. It is possible to select DAQ type and mode for different purposes.

There are six DAQ modules available in Snort;

- `Pcap`: Default mode, known as Sniffer mode.
- `Afpacket`: Inline mode, known as IPS mode.
- `Ipq`: Inline mode on Linux by using Netfilter. It replaces the snort_inline patch.  
- `Nfq`: Inline mode on Linux.
- `Ipfw`: Inline on OpenBSD and FreeBSD by using divert sockets, with the pf and ipfw firewalls.
- `Dump`: Testing mode of inline and normalisation.

The most popular modes are the default (pcap) and inline/IPS (Afpacket).

**Navigate to the "Step #6: Configure output plugins" section.**

This section manages the outputs of the IDS/IPS actions, such as logging and alerting format details. The default action prompts everything in the console application, so configuring this part will help you use the Snort more efficiently. 

**Navigate to the "Step #7: Customise your ruleset" section.**

| TAG NAME | INFO | EXAMPLE |
|:---:|:---:|:---:|
| # site specific rules | Hardcoded local and user-generated rules path. | include $RULE_PATH/local.rules |
| #include $RULE_PATH/ | Hardcoded default/downloaded rules path. | include $RULE_PATH/rulename |

> `Note` that "#" is commenting operator. You should uncomment a line to activate it.

---

## Task 11  Conclusion

In this room, we covered Snort, what it is, how it operates, and how to create and use the rules to investigate threats.

- Understanding and practising the fundamentals is crucial before creating advanced rules and using additional options.
- Do not create complex rules at once; try to add options step by step to notice possible syntax errors or any other problem easily.
- Do not reinvent the wheel; use it or modify/enhance it if there is a smooth rule.
- Take a backup of the configuration files before making any change.
- Never delete a rule that works properly. Comment it if you don't need it.
- Test newly created rules before migrating them to production.

Now, we invite you to complete the snort challenge room: [Snort Challenge - Live Attacks](https://tryhackme.com/room/snortchallenges1)

A great way to quickly recall snort rules and commands is to download and refer to the TryHackMe snort cheatsheet.

> - https://assets.tryhackme.com/cheatsheets/Snort%20Cheatsheet%20-%20TryHackMe.pdf


---
---

- [SNORTOLOGY 101 - THE ANATOMY OF A SNORT RULE](https://snort-org-site.s3.amazonaws.com/production/document_files/files/000/000/116/original/Snort_rule_infographic.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAU7AK5ITMJQBJPARJ%2F20221114%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20221114T140032Z&X-Amz-Expires=172800&X-Amz-SignedHeaders=host&X-Amz-Signature=fda964fbf1b18a907a8e4d8082da10336c2aec7bf8dfe9f67391283bb08dc903)
