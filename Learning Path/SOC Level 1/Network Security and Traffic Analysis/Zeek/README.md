![image](https://user-images.githubusercontent.com/51442719/202874615-a3b4a03e-ac1e-4e09-b58e-966b6867517a.png)

![image](https://user-images.githubusercontent.com/51442719/202874753-af704bef-2f7d-4b34-bba5-2f8ab1f0b7a9.png)

# [Zeek](https://tryhackme.com/room/zeekbro)
### Introduction to hands-on network monitoring and threat detection with Zeek (formerly Bro).

---

- [Task 1  Introduction](#task-1--introduction)
- [Task 2  Network Security Monitoring and Zeek](#task-2--network-security-monitoring-and-zeek)
- [Task 3  Zeek Logs](#task-3--zeek-logs)
- [Task 4  CLI Kung-Fu Recall: Processing Zeek Logs](#task-4--cli-kung-fu-recall-processing-zeek-logs)
- [Task 5  Zeek Signatures](#task-5--zeek-signatures)
- [Task 6  Zeek Scripts | Fundamentals](#task-6--zeek-scripts--fundamentals)
- [Task 7  Zeek Scripts | Scripts and Signatures](#task-7--zeek-scripts--scripts-and-signatures)
- [Task 8  Zeek Scripts | Frameworks](#task-8--zeek-scripts--frameworks)
- [Task 9  Zeek Scripts | Packages](#task-8--zeek-scripts--packages)
- [Task 10  Conclusion](#task-10--conclusion)

---

- `NSM` - Network Security Monitoring 

---

## Task 1  Introduction

![image](https://user-images.githubusercontent.com/51442719/202874775-1a262b20-34c2-4706-a351-3be1520e229c.png)

Zeek (formerly Bro) is an open-source and commercial network monitoring tool (traffic analyser).

[The official description](https://docs.zeek.org/en/master/about.html); "Zeek (formerly Bro) is the world's leading platform for network security monitoring. Flexible, open-source, and powered by defenders." "Zeek is a passive, open-source network traffic analyser. Many operators use Zeek as a network security monitor (NSM) to support suspicious or malicious activity investigations. Zeek also supports a wide range of traffic analysis tasks beyond the security domain, including performance measurement and troubleshooting."

The room aims to provide a general network monitoring overview and work with Zeek to investigate captured traffic. This room will expect you to have basic Linux familiarity and Network fundamentals (ports, protocols and traffic data). We suggest completing the "[Network Fundamentals](https://tryhackme.com/module/network-fundamentals)" path before starting working in this room. 

A VM is attached to this room. You don't need SSH or RDP; the room provides a "Split View" feature. Exercise files are located in the folder on the desktop. Log cleaner script "clear-logs.sh" is available in each exercise folder.


---

## Task 2  Network Security Monitoring and Zeek

![image](https://user-images.githubusercontent.com/51442719/202874806-6081eb83-5290-47bb-a2b0-c3b3855f7144.png)

### Introduction to Network Monitoring Approaches

Network monitoring is a set of management actions to watch/continuously overview and optionally save the network traffic for further investigation. This action aims to detect and reduce network problems, improve performance, and in some cases, increase overall productivity. It is a main part of the daily IT/SOC operations and differs from Network Security Monitoring (NSM) in its purpose.

#### Network Monitoring
Network monitoring is highly focused on IT assets like uptime (availability), device health and connection quality (performance), and network traffic balance and management (configuration). Monitoring and visualising the network traffic, troubleshooting, and root cause analysis are also part of the Network Monitoring process. This model is helpful for network administrators and usually doesn't cover identifying non-asset in-depth vulnerabilities and significant security concerns like internal threats and zero-day vulnerabilities. Usually, Network Monitoring is not within the SOC scope. It is linked to the enterprise IT/Network management team.

#### Network Security Monitoring
Network Security Monitoring is focused on network anomalies like rogue hosts, encrypted traffic, suspicious service and port usage, and malicious/suspicious traffic patterns in an intrusion/anomaly detection and response approach. Monitoring and visualising the network traffic and investigating suspicious events is a core part of Network Security Monitoring. This model is helpful for security analysts/incident responders, security engineers and threat hunters and covers identifying threats, vulnerabilities and security issues with a set of rules, signatures and patterns. Network Security Monitoring is part of the SOC, and the actions are separated between tier 1-2-3 analyst levels.

### What is ZEEK?
Zeek (formerly Bro) is an open-source and commercial passive Network Monitoring tool (traffic analysis framework) developed by Lawrence Berkeley Labs. Today, Zeek is supported by several developers, and Corelight provides an Enterprise-ready fork of Zeek. Therefore this tool is called both open source and commercial. The differences between the open-source version and the commercial version are detailed here.

Zeek differs from known monitoring and IDS/IPS tools by providing a wide range of detailed logs ready to investigate both for forensics and data analysis actions. Currently, Zeek provides 50+ logs in 7 categories.

### Zeek vs Snort
While both are called IDS/NIDS, it is good to know the cons and pros of each tool and use them in a specific manner. While there are some overlapping functionalities, they have different purposes for usage.

| Tool | Zeek | Snort |
|:---:|:---:|:---:|
| Capabilities | NSM and IDS framework. It is heavily focused on network analysis. It is more focused on specific threats to trigger alerts. The detection mechanism is focused on events. | An IDS/IPS system. It is heavily focused on signatures to detect vulnerabilities. The detection mechanism is focused on signature patterns and packets. |
| Cons | Hard to use. The analysis is done out of the Zeek, manually or by automation.  | Hard to detect complex threats. |
| Pros | It provides in-depth traffic visibility. Useful for threat hunting. Ability to detect complex threats. It has a scripting language and supports event correlation.  Easy to read logs. | Easy to write rules. Cisco supported rules. Community support. |
| Common Use Case | Network monitoring. In-depth traffic investigation. Intrusion detecting in chained events.  | Intrusion detection and prevention. Stop known attacks/threats. |

### Zeek Architecture

Zeek has two primary layers; "Event Engine" and "Policy Script Interpreter". The Event Engine layer is where the packets are processed; it is called the event core and is responsible for describing the event without focusing on event details. It is where the packages are divided into parts such as source and destination addresses, protocol identification, session analysis and file extraction. The Policy Script Interpreter layer is where the semantic analysis is conducted. It is responsible for describing the event correlations by using Zeek scripts.

![image](https://user-images.githubusercontent.com/51442719/202874853-7caafe30-222e-4074-a11e-3936c6ec4890.png)

### Zeek Frameworks
Zeek has several frameworks to provide extended functionality in the scripting layer. These frameworks enhance Zeek's flexibility and compatibility with other network components. Each framework focuses on the specific use case and easily runs with Zeek installation. For instance, we will be using the "Logging Framework" for all cases. Having ide on each framework's functionality can help users quickly identify an event of interest. 

#### Available Frameworks

| Logging | Notice | Input | Configuration | Intelligence |
|:---:|:---:|:---:|:---:|:---:|
| Cluster | Broker Communication | Supervisor | GeoLocation | File Analysis |
| Signature | Summary | NetControl | Packet Analysis | TLS Decryption |

You can read more on frameworks [here](https://docs.zeek.org/en/master/frameworks/index.html). 

### Zeek Outputs

As mentioned before, Zeek provides 50+ log files under seven different categories, which are helpful in various areas such as traffic monitoring, intrusion detection, threat hunting and web analytics. This section is not intended to discuss the logs in-depth. The logs are covered in TASK 3.

Once you run Zeek, it will automatically start investigating the traffic or the given pcap file and generate logs automatically. Once you process a pcap with Zeek, it will create the logs in the working directory. If you run the Zeek as a service, your logs will be located in the default log path. The default log path is:`/opt/zeek/logs/` 

### Working with Zeek
There are two operation options for Zeek. The first one is running it as a service, and the second option is running the Zeek against a pcap. Before starting working with Zeek, let's check the version of the Zeek instance with the following command: `zeek -v`

Now we are sure that we have Zeek installed. Let's start the Zeek as a service! To do this, we need to use the "ZeekControl" module, as shown below. The "ZeekControl" module requires superuser permissions to use. You can elevate the session privileges and switch to the superuser account to examine the generated log files with the following command: `sudo su`

Here we can manage the Zeek service and view the status of the service. Primary management of the Zeek service is done with three commands; "`status`", "`start`", and "`stop`". 

- ZeekControl Module

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

You can also use the "ZeekControl" mode with the following commands as well;
- `zeekctl status`
- `zeekctl start` 
- `zeekctl stop`

The only way to listen to the live network traffic is using Zeek as a service. Apart from using the Zeek as a network monitoring tool, we can also use it as a packet investigator. To do so, we need to process the pcap files with Zeek, as shown below. Once you process a pcap file, Zeek automatically creates log files according to the traffic.

In pcap processing mode, logs are saved in the working directory. You can view the generated logs using the `ls -l` command.  

- ZeekControl Module
```cmd
root@ubuntu$ zeek -C -r sample.pcap 

root@ubuntu$ ls -l
-rw-r--r-- 1 ubuntu ubuntu  11366 Mar 13 20:45 conn.log
-rw-r--r-- 1 ubuntu ubuntu    763 Mar 13 20:45 dhcp.log
-rw-r--r-- 1 ubuntu ubuntu   2918 Mar 13 20:45 dns.log
-rw-r--r-- 1 ubuntu ubuntu    254 Mar 13 20:45 packet_filter.log 
```

Main Zeek command line parameters are explained below;

| Parameter | Description |
|:---:|:---:|
| -r |  Reading option, read/process a pcap file. |
| -C |  Ignoring checksum errors. |
| -v |  Version information. |
| zeekctl | ZeekControl module. |

Investigating the generated logs will require command-line tools (cat, cut, grep sort, and uniq) and additional tools (zeek-cut). We will cover them in the following tasks.

---

## Task 3  Zeek Logs

![image](https://user-images.githubusercontent.com/51442719/202875391-d80a246e-b7c2-4495-9df8-6006a80b7be3.png)

### Zeek Logs

Zeek generates log files according to the traffic data. You will have logs for every connection in the wire, including the application level protocols and fields. Zeek is capable of identifying 50+ logs and categorising them into seven categories. Zeek logs are well structured and tab-separated ASCII files, so reading and processing them is easy but requires effort. You should be familiar with networking and protocols to correlate the logs in an investigation, know where to focus, and find a specific piece of evidence.



Each log output consists of multiple fields, and each field holds a different part of the traffic data. Correlation is done through a unique value called "UID". The "UID" represents the unique identifier assigned to each session.

#### Zeek logs in a nutshell;

| Category | Description | Log Files |
|:---:|:---:|:---:|
| Network | Network protocol logs. | conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.log, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log. |
| Files | File analysis result logs. | files.log, ocsp.log, pe.log, x509.log. |
| NetControl | Network control and flow logs. | netcontrol.log, netcontrol_drop.log, netcontrol_shunt.log, netcontrol_catch_release.log, openflow.log. |
| Detection | Detection and possible indicator logs. | intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log. |
| Network Observations | Network flow logs. | known_certs.log, known_hosts.log, known_modbus.log, known_services.log, software.log. |
| Miscellaneous | Additional logs cover external alerts, inputs and failures. | barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log. |
| Zeek Diagnostic | Zeek diagnostic logs cover system messages, actions and some statistics. | broker.log, capture_loss.log, cluster.log, config.log, loaded_scripts.log, packet_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log. |

Please refer to [Zeek's official documentation](https://docs.zeek.org/en/current/script-reference/log-files.html) and [Corelight log cheat sheet](https://corelight.com/about-zeek/zeek-data) for more information. Although there are multiple log files, some log files are updated daily, and some are updated in each session. Some of the most commonly used logs are explained in the given table.

| Update Frequency | Log Name | Description |
|:---:|:---:|:---:|
| Daily | known_hosts.log |  List of hosts that completed TCP handshakes. |
| Daily | known_services.log |  List of services used by hosts. |
| Daily | known_certs.log |  List of SSL certificates. |
| Daily | software.log |  List of software used on the network. |
| Per Session | notice.log |  Anomalies detected by Zeek. |
| Per Session | intel.log |  Traffic contains malicious patterns/indicators. |
| Per Session | signatures.log |  List of triggered signatures. |

This is too much protocol and log information! Yes, it is true; a difficulty of working with Zeek is having the required network knowledge and investigation mindset. Don't worry; you can have both of these and even more knowledge by working through TryHackMe paths. Just keep the streak! 

### Brief log usage primer table;

| Overall Info | Protocol Based | Detection | Observation |
|:---:|:---:|:---:|:---:|
| conn.log | http.log | notice.log | known_host.log |
| files.log | dns.log | signatures.log | known_services.log |
| intel.log | ftp.log | pe.log | software.log |
| loaded_scripts.log | ssh.log | traceroute.log | weird.log |

You can categorise the logs before starting an investigation. Thus, finding the evidence/anomaly you are looking for will be easier. The given table is a brief example of using multiple log files. You can create your working model or customise the given one. Make sure you read each log description and understand the purpose to know what to expect from the corresponding log file. Note that these are not the only ones to focus on. Investigated logs are highly associated with the investigation case type and hypothesis, so do not just rely only on the logs given in the example table!

The table shows us how to use multiple logs to identify anomalies and run an investigation by correlating across the available logs.

- `Overall Info`: The aim is to review the overall connections, shared files, loaded scripts and indicators at once. This is the first step of the investigation.
- `Protocol Based`: Once you review the overall traffic and find suspicious indicators or want to conduct a more in-depth investigation, you focus on a specific protocol.
- `Detection`: Use the prebuild or custom scripts and signature outcomes to support your findings by having additional indicators or linked actions. 
- `Observation`: The summary of the hosts, services, software, and unexpected activity statistics will help you discover possible missing points and conclude the investigation.


Remember, we mention the pros and cons of the Zeek logs at the beginning of this task. Now let's demonstrate the log viewing and identify the differences between them.

- `Recall 1`: Zeek logs are well structured and tab-separated ASCII files, so reading and processing them is easy but requires effort.
- `Recall 2`: Investigating the generated logs will require command-line tools (cat, cut, grep sort, and uniq) and additional tools (zeek-cut). 


### Opening a Zeek log with a text editor and built-in commands;

![image](https://user-images.githubusercontent.com/51442719/202875494-1f57c8a9-ca51-4f0d-be0f-6313c495d7ee.png)

The above image shows that reading the logs with tools is not enough to spot an anomaly quickly. Logs provide a vast amount of data to investigate and correlate. You will need to have technical knowledge and event correlation ability to carry out an investigation. It is possible to use external visualisation and correlation tools such as ELK and Splunk. We will focus on using and processing the logs with a hands-on approach in this room.

In addition to Linux command-line tools, one auxiliary program called `zeek-cut` reduces the effort of extracting specific columns from log files. Each log file provides "field names" in the beginning. This information will help you while using `zeek-cut`. Make sure that you use the "fields" and not the "types".

| Tool/Auxilary Name | Purpose |
|:---:|:---:|
| Zeek-cut | Cut specific columns from zeek logs. |

Let's see the "zeek-cut" in action. Let's extract the uid, protocol, source and destination hosts, and source and destination ports from the conn.log. We will first read the logs with the `cat` command and then extract the event of interest fields with `zeek-cut` auxiliary to compare the difference.

- zeek-cut usage example
```cmd
root@ubuntu$ cat conn.log 
...
#fields	ts	uid	id.orig_h	id.orig_p	id.resp_h	id.resp_p	proto	service	duration	orig_bytes	resp_bytes	conn_state	local_orig	local_resp	missed_bytes	history	orig_pkts	orig_ip_bytes	resp_pkts	resp_ip_bytes	tunnel_parents
#types	time	string	addr	port	addr	port	enum	string	interval	count	count	string	bool	bool	count	string	count	count	count	count	set[string]
1488571051.943250	CTMFXm1AcIsSnq2Ric	192.168.121.2	51153	192.168.120.22	53	udp	dns	0.001263	36	106	SF	-	-0	Dd	1	64	1	134	-
1488571038.380901	CLsSsA3HLB2N6uJwW	192.168.121.10	50080	192.168.120.10	514	udp	-	0.000505	234	0	S0	-	-0	D	2	290	0	0	-

root@ubuntu$ cat conn.log | zeek-cut uid proto id.orig_h id.orig_p id.resp_h id.resp_p 
CTMFXm1AcIsSnq2Ric	udp	192.168.121.2	51153	192.168.120.22	53
CLsSsA3HLB2N6uJwW	udp	192.168.121.10	50080	192.168.120.10	514
```

As shown in the above output, the "zeek-cut" auxiliary provides massive help to extract specific fields with minimal effort. Now take time to read log formats, practice the log reading/extracting operations and answer the questions.


---

## Task 4  CLI Kung-Fu Recall: Processing Zeek Logs

---

## Task 5  Zeek Signatures

---

## Task 6  Zeek Scripts | Fundamentals

---

## Task 7  Zeek Scripts | Scripts and Signatures

---

## Task 8  Zeek Scripts | Frameworks

---

## Task 9  Zeek Scripts | Packages

---

## Task 10  Conclusion
