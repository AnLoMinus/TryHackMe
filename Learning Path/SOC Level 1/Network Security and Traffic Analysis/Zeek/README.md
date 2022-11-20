![image](https://user-images.githubusercontent.com/51442719/202874753-af704bef-2f7d-4b34-bba5-2f8ab1f0b7a9.png)

# [Zeek](https://tryhackme.com/room/zeekbro)
### Introduction to hands-on network monitoring and threat detection with Zeek (formerly Bro).

![image](https://user-images.githubusercontent.com/51442719/202874615-a3b4a03e-ac1e-4e09-b58e-966b6867517a.png)

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

![image](https://user-images.githubusercontent.com/51442719/202875587-19fcf48b-f746-4c26-9a8f-40ef6ece3a7a.png)

### CLI Kung-Fu Recall: Processing Zeek Logs

Graphical User Interfaces (GUI) are handy and good for accomplishing tasks and processing information quickly. There are multiple advantages of GUIs, especially when processing the information visually. However, when processing massive amounts of data, GUIs are not stable and as effective as the CLI (Command Line Interface) tools.

The critical point is: What if there is no "function/button/feature" for what you want to find/view/extract?

Having the power to manipulate the data at the command line is a crucial skill for analysts. Not only in this room but each time you deal with packets, you will need to use command-line tools, Berkeley Packet Filters (BPF) and regular expressions to find/view/extract the data you are looking for. This task provides quick cheat-sheet like information to help you write CLI queries for your event of interest.

<table>
<thead>
  <tr>
    <th>Category<br></th>
    <th>Command Purpose and Usage <br></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Basics<br></td>
    <td>View the command history:<br>ubuntu@ubuntu$ history<br><br>Execute the 10th command in history:<br>ubuntu@ubuntu$ !10<br><br>Execute the previous command:<br>ubuntu@ubuntu$ !!</td>
  </tr>
  <tr>
    <td>Read File</td>
    <td><br>Read sample.txt file:<br>ubuntu@ubuntu$ cat sample.txt<br><br>Read the first 10 lines of the file:<br>ubuntu@ubuntu$ head sample.txt<br><br>Read the last 10 lines of the file:<br>ubuntu@ubuntu$ tail sample.txt</td>
  </tr>
  <tr>
    <td>Advanced<br></td>
    <td><br>Print line 11:<br>ubuntu@ubuntu$ cat test.txt | sed -n '11p'<br><br>Print lines between 10-15:<br>ubuntu@ubuntu$ cat test.txt | sed -n '10,15p'<br><br>Print lines below 11:<br>ubuntu@ubuntu$ cat test.txt | awk 'NR &lt; 11 {print $0}'<br><br>Print line 11:<br>ubuntu@ubuntu$ cat test.txt | awk 'NR == 11 {print $0}'</td>
  </tr>
  <tr>
    <td>Special</td>
    <td>Filter specific fields of Zeek logs:<br>ubuntu@ubuntu$ cat signatures.log | zeek-cut uid src_addr dst_addr</td>
  </tr>
  <tr>
    <td>Use Case</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>sort | uniq</td>
    <td>Remove duplicate values.<br></td>
  </tr>
  <tr>
    <td>sort | uniq -c </td>
    <td>Remove duplicates and count the number of occurrences for each value.<br></td>
  </tr>
  <tr>
    <td>sort -nr</td>
    <td>Sort values numerically and recursively.</td>
  </tr>
  <tr>
    <td>rev</td>
    <td>Reverse string characters.</td>
  </tr>
  <tr>
    <td>cut -f 1</td>
    <td>Cut field 1.</td>
  </tr>
  <tr>
    <td>cut -d '.' -f 1-2</td>
    <td>Split the string on every dot and print keep the first two fields.</td>
  </tr>
  <tr>
    <td>grep -v 'test'</td>
    <td>Display lines that  don't match the "test" string.</td>
  </tr>
  <tr>
    <td>grep -v -e 'test1' -e 'test2'</td>
    <td>Display lines that don't match one or both "test1" and "test2" strings.</td>
  </tr>
  <tr>
    <td>file </td>
    <td>View file information.</td>
  </tr>
  <tr>
    <td>grep -rin Testvalue1 * | column -t | less -S</td>
    <td>Search the "Testvalue1" string everywhere, organise column spaces and view the output with less.</td>
  </tr>
</tbody>
</table>


---

## Task 5  Zeek Signatures

![image](https://user-images.githubusercontent.com/51442719/202876215-89beb08b-3800-4b04-be9f-be541e679f11.png)

### Zeek Signatures

Zeek supports signatures to have rules and event correlations to find noteworthy activities on the network. Zeek signatures use low-level pattern matching and cover conditions similar to Snort rules. Unlike Snort rules, Zeek rules are not the primary event detection point. Zeek has a scripting language and can chain multiple events to find an event of interest. We focus on the signatures in this task, and then we will focus on Zeek scripting in the following tasks.

Zeek signatures are composed of three logical paths; signature id, conditions and action. The signature breakdown is shown in the table below;

| Signature id |  Unique signature name. |
|:---:|---|
| Conditions | Header: Filtering the packet headers for specific source and destination addresses, protocol and port numbers.Content: Filtering the packet payload for specific value/pattern. |
| Action | Default action: Create the "signatures.log" file in case of a signature match. Additional action: Trigger a Zeek script. |

Now let's dig more into the Zeek signatures. The below table provides the most common conditions and filters for the Zeek signatures.

<table>
<thead>
  <tr>
    <th>Condition Field</th>
    <th>Available Filters</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Header</td>
    <td>src-ip: Source IP.dst-ip: Destination IP.src-port: Source port.dst-port: Destination port.ip-proto: Target protocol. Supported protocols; TCP, UDP, ICMP, ICMP6, IP, IP6</td>
  </tr>
  <tr>
    <td>Content</td>
    <td>payload: Packet payload.<br>http-request: Decoded HTTP requests.<br>http-request-header: Client-side HTTP headers.<br>http-request-body: Client-side HTTP request bodys.<br>http-reply-header: Server-side HTTP headers.<br>http-reply-body: Server-side HTTP request bodys.<br>ftp: Command line input of FTP sessions.<br></td>
  </tr>
  <tr>
    <td>Context</td>
    <td>same-ip: Filtering the source and destination addresses for duplication.<br></td>
  </tr>
  <tr>
    <td>Action</td>
    <td>event: Signature match message.<br></td>
  </tr>
  <tr>
    <td>Comparison<br>Operators</td>
    <td>==, !=, &lt;, &lt;=, &gt;, &gt;=</td>
  </tr>
  <tr>
    <td>NOTE!</td>
    <td> Filters accept string, numeric and regex values.</td>
  </tr>
</tbody>
</table>

```cmd
Run Zeek with signature file
ubuntu@ubuntu$ zeek -C -r sample.pcap -s sample.sig
```

<table>
<thead>
  <tr>
    <th>Zeek signatures use the ".sig" extension.</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>-C: Ignore checksum errors.<br> -r: Read pcap file.<br>-s: Use signature file. </td>
  </tr>
</tbody>
</table>

### Example | Cleartext Submission of Password
Let's create a simple signature to detect HTTP cleartext passwords.

- Sample Signature
```cmd
signature http-password {
     ip-proto == tcp
     dst_port == 80
     payload /.*password.*/
     event "Cleartext Password Found!"
}

# signature: Signature name.
# ip-proto: Filtering TCP connection.
# dst-port: Filtering destination port 80.
# payload: Filtering the "password" phrase.
# event: Signature match message.
```

Remember, Zeek signatures support regex. Regex ".*" matches any character zero or more times. The rule will match when a "password" phrase is detected in the packet payload. Once the match occurs, Zeek will generate an alert and create additional log files (signatures.log and notice.log).

- Signature Usage and Log Analysis
```cmd
ubuntu@ubuntu$ zeek -C -r http.pcap -s http-password.sig 
ubuntu@ubuntu$ ls
clear-logs.sh  conn.log  files.log  http-password.sig  http.log  http.pcap  notice.log  packet_filter.log  signatures.log

ubuntu@ubuntu$ cat notice.log  | zeek-cut id.orig_h id.resp_h msg 
10.10.57.178	44.228.249.3	10.10.57.178: Cleartext Password Found!
10.10.57.178	44.228.249.3	10.10.57.178: Cleartext Password Found!

ubuntu@ubuntu$ cat signatures.log | zeek-cut src_addr dest_addr sig_id event_msg 
10.10.57.178		http-password	10.10.57.178: Cleartext Password Found!
10.10.57.178		http-password	10.10.57.178: Cleartext Password Found!
```

As shown in the above terminal output, the signatures.log and notice.log provide basic details and the signature message. Both of the logs also have the application banner field. So it is possible to know where the signature match occurs. Let's look at the application banner!

- Log Analysis
```cmd
ubuntu@ubuntu$ cat signatures.log | zeek-cut sub_msg
POST /userinfo.php HTTP/1.1\x0d\x0aHost: testphp.vulnweb.com\x0d\x0aUser-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:98.0) Gecko/20100101 Firefox/...

ubuntu@ubuntu$ cat notice.log  | zeek-cut sub
POST /userinfo.php HTTP/1.1\x0d\x0aHost: testphp.vulnweb.com\x0d\x0aUser-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:98.0) Gecko/20100101 Firefox/...
```

We will demonstrate only one log file output to avoid duplication after this point. You can practice discovering the event of interest by analysing notice.log and signatures.log.

### Example | FTP Brute-force
Let's create another rule to filter FTP traffic. This time, we will use the FTP content filter to investigate command-line inputs of the FTP traffic. The aim is to detect FTP "admin" login attempts. This basic signature will help us identify the admin login attempts and have an idea of possible admin account abuse or compromise events.

- Sample Signature
```cmd
signature ftp-admin {
     ip-proto == tcp
     ftp /.*USER.*dmin.*/
     event "FTP Admin Login Attempt!"
}
```

Let's run the Zeek with the signature and investigate the signatures.log and notice.log.

```cmd
FTP Signature
ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig
ubuntu@ubuntu$ cat signatures.log | zeek-cut src_addr dst_addr event_msg sub_msg | sort -r| uniq
10.234.125.254	10.121.70.151	10.234.125.254: FTP Admin Login Attempt!	USER administrator
10.234.125.254	10.121.70.151	10.234.125.254: FTP Admin Login Attempt!	USER admin
```

Our rule shows us that there are multiple logging attempts with account names containing the "admin" phrase. The output gives us great information to notice if there is a brute-force attempt for an admin account.

This signature can be considered a case signature. While it is accurate and works fine, we need global signatures to detect the "known threats/anomalies". We will need those case-based signatures for significant and sophistical anomalies like zero-days and insider attacks in the real-life environment. Having individual rules for each case will create dozens of logs and alerts and cause missing the real anomaly. The critical point is logging logically, not logging everything.

We can improve our signature by not limiting the focus only to an admin account. In that case, we need to know how the FTP protocol works and the default response codes. If you don't know these details, please refer to [RFC documentation](https://datatracker.ietf.org/doc/html/rfc765). 

Let's optimise our rule and make it detect all possible FTP brute-force attempts.

This signature will create logs for each event containing "FTP 530 response", which allows us to track the login failure events regardless of username. 

- Sample Signature
```cmd
signature ftp-brute {
     ip-proto == tcp
     payload /.*530.*Login.*incorrect.*/
     event "FTP Brute-force Attempt"
}
```

Zeek signature files can consist of multiple signatures. Therefore we can have one file for each protocol/situation/threat type. Let's demonstrate this feature in our global rule.

- Sample Signature
```cmd
signature ftp-username {
    ip-proto == tcp
    ftp /.*USER.*/
    event "FTP Username Input Found!"
}

signature ftp-brute {
    ip-proto == tcp
     payload /.*530.*Login.*incorrect.*/
    event "FTP Brute-force Attempt!"
}
```

Let's merge both of the signatures in a single file. We will have two different signatures, and they will generate alerts according to match status. The result will show us how we benefit from this action. Again, we will need the "CLI Kung-Fu" skills to extract the event of interest.



This rule should show us two types of alerts and help us to correlate the events by having "FTP Username Input" and "FTP Brute-force Attempt" event messages. Let's investigate the logs. We're grepping the logs in range 1001-1004 to demonstrate that the first rule matches two different accounts (admin and administrator). 

- FTP Signature
```cmd
ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig
ubuntu@ubuntu$ cat notice.log | zeek-cut uid id.orig_h id.resp_h msg sub | sort -r| nl | uniq | sed -n '1001,1004p'
  1001	CeMYiaHA6AkfhSnd	10.234.125.254	10.121.70.151	10.234.125.254: FTP Username Input Found!	USER admin
  1002	CeMYiaHA6AkfhSnd	10.234.125.254	10.121.70.151	10.121.70.151: FTP Brute-force Attempt!	530 Login incorrect.
  1003	CeDTDZ2erDNF5w7dyf	10.234.125.254	10.121.70.151	10.234.125.254: FTP Username Input Found!	USER administrator
  1004	CeDTDZ2erDNF5w7dyf	10.234.125.254	10.121.70.151	10.121.70.151: FTP Brute-force Attempt!	530 Login incorrect.
```

### Snort Rules in Zeek?
While Zeek was known as Bro, it supported Snort rules with a script called snort2bro, which converted Snort rules to Bro signatures. However, after the rebranding, workflows between the two platforms have changed. [The official Zeek document](https://docs.zeek.org/en/master/frameworks/signatures.html) mentions that the script is no longer supported and is not a part of the Zeek distribution.

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
