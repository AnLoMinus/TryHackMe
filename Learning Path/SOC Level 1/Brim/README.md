![image](https://user-images.githubusercontent.com/51442719/203181214-53c0ac19-53d6-4887-9e21-fc22d975a0de.png)

# [Brim](https://tryhackme.com/room/brim)

![image](https://user-images.githubusercontent.com/51442719/203181202-961d23e2-2fe3-4197-be96-864894c7bf6e.png)

### Learn and practice log investigation, pcap analysis and threat hunting with Brim.

---

- [Task 1  Introduction](#task-1--introduction)
- [Task 2  What is Brim?](#task-2--what-is-brim)
- [Task 3  The Basics](#task-3--the-basics)
- [Task 4  Default Queries](#task-4--default-queries)
- [Task 5  Use Cases](#task-5-use-cases)
- [Task 6  Exercise: Threat Hunting with Brim | Malware C2 Detection]()
- [Task 7  Exercise: Threat Hunting with Brim | Crypto Mining]()
- [Task 8  Conclusion]()

---

## Task 1  Introduction

[BRIM](https://www.brimdata.io/) is an open-source desktop application that processes pcap files and logs files. Its primary focus is providing search and analytics. In this room, you will learn how to use Brim, process pcap files and investigate log files to find the needle in the haystack! This room expects you to be familiar with basic security concepts and processing Zeek log files. We suggest completing the "[Network Fundamentals](https://tryhackme.com/module/network-fundamentals)" path and the "[Zeek room](https://tryhackme.com/room/zeekbro)" before starting working in this room. 

A VM is attached to this room. You don't need SSH or RDP; the room provides a "Split View" feature. Exercise files are located in the folder on the desktop. 
> `NOTE`: DO NOT directly interact with any domains and IP addresses in this room. 

![image](https://user-images.githubusercontent.com/51442719/203181052-e896c700-534e-437d-91ae-1a10897c130c.png)

--- 

## Task 2  What is Brim?

### What is Brim?

Brim is an open-source desktop application that processes pcap files and logs files, with a primary focus on providing search and analytics. It uses the Zeek log processing format. It also supports Zeek signatures and Suricata Rules for detection.

#### It can handle two types of data as an input;

- `Packet Capture Files`: Pcap files created with tcpdump, tshark and Wireshark like applications.
- `Log Files`: Structured log files like Zeek logs.

#### Brim is built on open-source platforms:

- `Zeek`: Log generating engine.
- `Zed Language`: Log querying language that allows performing keywoırd searches with filters and pipelines.
- `ZNG Data Format`: Data storage format that supports saving data streams.
- `Electron and React`: Cross-platform UI.

#### Why Brim?

Ever had to investigate a big pcap file? Pcap files bigger than one gigabyte are cumbersome for Wireshark. Processing big pcaps with tcpdump and Zeek is efficient but requires time and effort. Brim reduces the time and effort spent processing pcap files and investigating the log files by providing a simple and powerful GUI application.

#### Brim vs Wireshark vs Zeek

While each of them is powerful and useful, it is good to know the strengths and weaknesses of each tool and which one to use for the best outcome. As a traffic capture analyser, some overlapping functionalities exist, but each one has a unique value for different situations.

The common best practice is handling medium-sized pcaps with Wireshark, creating logs and correlating events with Zeek, and processing multiple logs in Brim.

| Brim | Wireshark | Zeek |  |
|:---:|:---:|:---:|---|
| Purpose | Pcap processing; event/stream and log investigation. | Traffic sniffing. Pcap processing; packet and stream investigation. | Pcap processing; event/stream and log investigation. |
| GUI | ✔ | ✔ | ✖ |
| Sniffing | ✖ | ✔ | ✔ |
| Pcap processing | ✔ | ✔ | ✔ |
| Log processing | ✔ | ✖ | ✔ |
| Packet decoding | ✖ | ✔ | ✔ |
| Filtering | ✔ | ✔ | ✔ |
| Scripting | ✖ | ✖ | ✔ |
| Signature Support | ✔ | ✖ | ✔ |
| Statistics | ✔ | ✔ | ✔ |
| File Extraction | ✖ | ✔ | ✔ |
| Handling  pcaps over 1GB | Medium performance | Low performance | Good performance |
| Ease of Management | 4/5 | 4/5 | 3/5 |

--- 

## Task 3  The Basics

### Landing Page
Once you open the application, the landing page loads up. The landing page has three sections and a file importing window. It also provides quick info on supported file formats.

- `Pools`: Data resources, investigated pcap and log files.
- `Queries`: List of available queries.
- `History`: List of launched queries.

### Pools and Log Details
Pools represent the imported files. Once you load a pcap, Brim processes the file and creates Zeek logs, correlates them, and displays all available findings in a timeline, as shown in the image below. 

![image](https://user-images.githubusercontent.com/51442719/203181883-d41d5b18-d0ec-4cee-91eb-0ab101c386b3.png)

The timeline provides information about capture start and end dates. Brim also provides information fields. You can hover over fields to have more details on the field. The above image shows a user hovering over the Zeek's conn.log file and uid value. This information will help you in creating custom queries. The rest of the log details are shown in the right pane and provides details of the log file fields. Note that you can always export the results by using the export function located near the timeline.

![image](https://user-images.githubusercontent.com/51442719/203181892-4df5a8ef-c57d-4b80-85f5-73d8ad57b4d0.png)

You can correlate each log entry by reviewing the correlation section at the log details pane (shown on the left image). This section provides information on the source and destination addresses, duration and associated log files. This quick information helps you answer the "Where to look next?" question and find the event of interest and linked evidence.

You can also right-click on each field to filter and accomplish a list of tasks.

- Filtering values
- Counting fields
- Sorting (A-Z and Z-A)
- Viewing details 
- Performing whois lookup on IP address
- Viewing the associated packets in Wireshark

The image below demonstrates how to perform whois lookup and Wireshark packet inspection.

![image](https://user-images.githubusercontent.com/51442719/203181942-dc0aef37-7e51-4ed1-9272-1f5bdc773722.png)

### Queries and History

Queries help us to correlate finding and find the event of the interest. History stores executed queries.


The image on the left demonstrates how to browse the queries and load a specific query from the library.

Queries can have names, tags and descriptions. Query library lists the query names, and once you double-click, it passes the actual query to the search bar.

You can double-click on the query and execute it with ease. Once you double-click on the query, the actual query appears on the search bar and is listed under the history tab.

The results are shown under the search bar. In this case, we listed all available log sources created by Brim. In this example, we only insert a pcap file, and it automatically creates nine types of Zeek log files. 

Brim has 12 premade queries listed under the "Brim" folder. These queries help us discover the Brim query structure and accomplish quick searches from templates.  You can add new queries by clicking on the "+" button near the "Queries" menu.

![image](https://user-images.githubusercontent.com/51442719/203182030-64f81060-cc86-4132-b395-96b34c06c8f8.png)

![image](https://user-images.githubusercontent.com/51442719/203182054-402238ca-5ba1-493c-b633-ccbc108cc4b1.png)


--- 

## Task 4  Default Queries

### Default Queries

We mentioned that Brim had 12 premade queries in the previous task. Let's see them in action! Now, open Brim, import the sample pcap and go through the walkthrough.

![image](https://user-images.githubusercontent.com/51442719/203185696-d19d83fc-b5af-4742-9f06-687e0e19ffb7.png)

### Reviewing Overall Activity
This query provides general information on the pcap file. The provided information is valuable for accomplishing further investigation and creating custom queries. It is impossible to create advanced or case-specific queries without knowing the available log files.

The image on the left shows that there are 20 logs generated for the provided pcap file. 

#### Windows Specific Networking Activity

This query focuses on Windows networking activity and details the source and destination addresses and named pipe, endpoint and operation detection. The provided information helps investigate and understand specific Windows eve

![image](https://user-images.githubusercontent.com/51442719/203185853-2880a7fe-d910-444f-9f43-9c0ca0282361.png)

#### Unique Network Connections and Transferred Data

These two queries provide information on unique connections and connection-data correlation. The provided info helps analysts detect weird and malicious connections and suspicious and beaconing activities. The uniq list provides a clear list of unique connections that help identify anomalies. The data list summarises the data transfer rate that supports the anomaly investigation hypothesis.

![image](https://user-images.githubusercontent.com/51442719/203185908-7beb6fa0-68ab-4c84-87b7-7a73e6383caa.png)

#### DNS and HTTP Methods

These queries provide the list of the DNS queries and HTTP methods. The provided information helps analysts to detect anomalous DNS and HTTP traffic. You can also narrow the search by viewing the "HTTP POST" requests with the available query and modifying it to view the "HTTP GET" methods.

![image](https://user-images.githubusercontent.com/51442719/203185980-cce63d0e-a72b-43cd-b020-2fc5620e4d19.png)

#### File Activity

This query provides the list of the available files. It helps analysts to detect possible data leakage attempts and suspicious file activity. The query provides info on the detected file MIME and file name and hash values (MD5, SHA1).

![image](https://user-images.githubusercontent.com/51442719/203186012-a2257f42-78ba-4d4a-9385-2c408f5c1dd6.png)

#### IP Subnet Statistics

This query provides the list of the available IP subnets. It helps analysts detect possible communications outside the scope and identify out of ordinary IP addresses. 

![image](https://user-images.githubusercontent.com/51442719/203186041-82fa65b5-8f2b-45d5-aa99-594ed6b044cf.png)

#### Suricata Alerts

These queries provide information based on Suricata rule results. Three different queries are available to view the available logs in different formats (category-based, source and destination-based, and subnet based). 

> `Note`: Suricata is an open-source threat detection engine that can act as a rule-based Intrusion Detection and Prevention System. It is developed by the Open Information Security Foundation (OISF). Suricata works and detects anomalies in a similar way to Snort and can use the same signatures. 

![image](https://user-images.githubusercontent.com/51442719/203186078-784f102b-b640-445e-930f-de87a87fa085.png)

--- 

## Task 5  Use Cases

### Custom Queries and Use Cases

There are a variety of use case examples in traffic analysis. For a security analyst, it is vital to know the common patterns and indicators of anomaly or malicious traffic. In this task, we will cover some of them. Let's review the basics of the Brim queries before focusing on the custom and advanced ones.

#### Brim Query Reference

<table>
<thead>
  <tr>
    <th>Purpose</th>
    <th>Syntax</th>
    <th>Example Query</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Basic search </td>
    <td>You can search any string and numeric value. </td>
    <td><br>Find logs containing an IP address or any value.10.0.0.1<br></td>
  </tr>
  <tr>
    <td>Logical operators </td>
    <td>Or, And, Not. </td>
    <td><br>Find logs contain three digits of an IP AND NTP keyword.192 and NTP<br></td>
  </tr>
  <tr>
    <td>Filter values</td>
    <td>"field name" == "value"</td>
    <td><br>Filter source IP.id.orig_h==192.168.121.40<br></td>
  </tr>
  <tr>
    <td>List specific log file contents<br></td>
    <td>_path=="log name"<br></td>
    <td><br>List the contents of the conn log file._path=="conn"<br></td>
  </tr>
  <tr>
    <td>Count field values </td>
    <td>count () by "field"</td>
    <td><br>Count the number of the available log files.count () by _path<br></td>
  </tr>
  <tr>
    <td>Sort findings</td>
    <td>sort</td>
    <td><br>Count the number of the available log files and sort recursively.count () by _path | sort -r<br></td>
  </tr>
  <tr>
    <td>Cut specific field from a log file</td>
    <td>_path=="conn" | cut "field name"</td>
    <td><br>Cut the source IP, destination port and destination IP addresses from the conn log file._path=="conn" | cut id.orig_h, id.resp_p, id.resp_h<br></td>
  </tr>
  <tr>
    <td>List unique values</td>
    <td>uniq</td>
    <td>Show the unique network connections. <br>_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h | sort | uniq</td>
  </tr>
</tbody>
</table>

> `Note`: It is highly suggested to use field names and filtering options and not rely on the blind/irregular search function. Brim provides great indexing of log sources, but it is not performing well in irregular search queries. The best practice is always to use the field filters to search for the event of interest.

<table>
<thead>
  <tr>
    <th>Communicated Hosts<br></th>
    <th>Identifying the list of communicated hosts is the first step of the investigation. Security analysts need to know which hosts are actively communicating on the network to detect any suspicious and abnormal activity in the first place. This approach will help analysts to detect possible access violations, exploitation attempts and malware infections.<br>Query: _path=="conn" | cut id.orig_h, id.resp_h | sort | uniq<br></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Frequently Communicated Hosts<br></td>
    <td>After having the list of communicated hosts, it is important to identify which hosts communicate with each other most frequently. This will help security analysts to detect possible data exfiltration, exploitation and backdooring activities.<br>Query: _path=="conn" | cut id.orig_h, id.resp_h | sort | uniq -c | sort -r<br></td>
  </tr>
  <tr>
    <td>Most Active Ports<br></td>
    <td>Suspicious activities are not always detectable in the first place. Attackers use multiple ways of hiding and bypassing methods to avoid detection. However, since the data is evidence, it is impossible to hide the packet traces. Investigating the most active ports will help analysts to detect silent and well-hidden anomalies by focusing on the data bus and used services. <br>Query: _path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count<br><br>Query:  _path=="conn" | cut id.orig_h, id.resp_h, id.resp_p, service | sort id.resp_p | uniq -c | sort -r <br></td>
  </tr>
  <tr>
    <td>Long Connections<br></td>
    <td>For security analysts, the long connections could be the first anomaly indicator. If the client is not designed to serve a continuous service, investigating the connection duration between two IP addresses can reveal possible anomalies like backdoors.<br>Query: _path=="conn" | cut id.orig_h, id.resp_p, id.resp_h, duration | sort -r duration<br></td>
  </tr>
  <tr>
    <td>Transferred Data <br></td>
    <td>Another essential point is calculating the transferred data size. If the client is not designed to serve and receive files and act as a file server, it is important to investigate the total bytes for each connection. Thus, analysts can distinguish possible data exfiltration or suspicious file actions like malware downloading and spreading.<br>Query: _path=="conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes</td>
  </tr>
  <tr>
    <td>DNS and HTTP Queries<br></td>
    <td>Identifying suspicious and out of ordinary domain connections and requests is another significant point for a security analyst. Abnormal connections can help detect C2 communications and possible compromised/infected hosts. Identifying the suspicious DNS queries and HTTP requests help security analysts to detect malware C2 channels and support the investigation hypothesis.<br><br>Query: _path=="dns" | count () by query | sort -r<br><br>Query: _path=="http" | count () by uri | sort -r</td>
  </tr>
  <tr>
    <td>Suspicious Hostnames<br></td>
    <td>Identifying suspicious and out of ordinary hostnames helps analysts to detect rogue hosts. Investigating the DHCP logs provides the hostname and domain information.<br>Query: _path=="dhcp" | cut host_name, domain<br></td>
  </tr>
  <tr>
    <td>Suspicious IP Addresses<br></td>
    <td>For security analysts, identifying suspicious and out of ordinary IP addresses is essential as identifying weird domain addresses. Since the connection logs are stored in one single log file (conn), filtering IP addresses is more manageable and provides more reliable results.<br>Query: _path=="conn" | put classnet := network_of(id.resp_h) | cut classnet | count() by classnet | sort -r<br></td>
  </tr>
  <tr>
    <td>Detect Files<br></td>
    <td>Investigating transferred files is another important point of traffic investigation. Performing this hunt will help security analysts to detect the transfer of malware or infected files by correlating the hash values. This act is also valuable for detecting transferring of sensitive files.<br>Query: filename!=null<br></td>
  </tr>
  <tr>
    <td>SMB Activity<br></td>
    <td>Another significant point is investigating the SMB activity. This will help analysts to detect possible malicious activities like exploitation, lateral movement and malicious file sharing. When running an investigation, it is suggested to ask, "What is going on in SMB?".<br>Query: _path=="dce_rpc" OR _path=="smb_mapping" OR _path=="smb_files"</td>
  </tr>
  <tr>
    <td>Known Patterns<br></td>
    <td>Known patterns represent alerts generated by security solutions. These alerts are generated against the common attack/threat/malware patterns and known by endpoint security products, firewalls and IDS/IPS solutions. This data source highly relies on available signatures, attacks and anomaly patterns. Investigating available log sources containing alerts is vital for a security analyst.<br>Brim supports the Zeek and Suricata logs, so any anomaly detected by these products will create a log file. Investigating these log files can provide a clue where the analyst should focus.<br>Query: event_type=="alert" or _path=="notice" or _path=="signatures"</td>
  </tr>
</tbody>
</table>

--- 

## Task 6  Exercise: Threat Hunting with Brim | Malware C2 Detection

### Threat Hunting with Brim | Malware C2 Detection

It is just another malware campaign spread with CobaltStrike. We know an employee clicks on a link, downloads a file, and then network speed issues and anomalous traffic activity arises. Now, open Brim, import the sample pcap and go through the walkthrough.

#### Let's investigate the traffic sample to detect malicious C2 activities!
 
![image](https://user-images.githubusercontent.com/51442719/203445477-3b95e4fd-82fb-4fed-af93-7728bc387a72.png)

Let's look at the available logfiles first to see what kind of data artefact we could have. The image on the left shows that we have many alternative log files we could rely on. Let's review the frequently communicated hosts before starting to investigate individual logs.

- Query: - `cut id.orig_h, id.resp_p, id.resp_h | sort  | uniq -c | sort -r count`

![image](https://user-images.githubusercontent.com/51442719/203445680-3413ecf8-783b-4611-9fa4-b042c01f27de.png)

This query provides sufficient data that helped us decide where to focus. The IP addresses "10.22.xx" and "104.168.xx" draw attention in the first place. Let's look at the port numbers and available services before focusing on the suspicious IP address and narrowing our search.

- Query: - `_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count`

![image](https://user-images.githubusercontent.com/51442719/203445867-6f6ffb46-b25a-4f8a-af01-52440a15492a.png)

Nothing extremely odd in port numbers, but there is a massive DNS record available. Let's have a closer look.

- Query: - `_path=="dns" | count() by query | sort -r`

![image](https://user-images.githubusercontent.com/51442719/203445950-a2499e05-3c13-48b9-828c-704ca1319a6d.png)

There are out of ordinary DNS queries. Let's enrich our findings by using VirusTotal to identify possible malicious domains.

![image](https://user-images.githubusercontent.com/51442719/203446037-5bfda7b4-38b4-4411-bd82-d77455231dc2.png)

We have detected two additional malicious IP addresses (we have the IP 45.147.xx from the log files and gathered the 68.138.xx and 185.70.xx from VirusTotal) linked with suspicious DNS queries with the help of external research. Let's look at the HTTP requests before narrowing down our investigation with the found malicious IP addresses.

- Query:  `_path=="http" | cut id.orig_h, id.resp_h, id.resp_p, method, host, uri | uniq -c | sort value.uri`

![image](https://user-images.githubusercontent.com/51442719/203446086-88efec0d-6b6d-412c-8cf9-1da729d9e120.png)

We detect a file download request from the IP address we assumed as malicious. Let's validate this idea with VirusTotal and validate our hypothesis. 

![image](https://user-images.githubusercontent.com/51442719/203446163-f8c14f0c-5360-491e-b69d-2a668caccc76.png)

VirusTotal results show that the IP address "104.xx" is linked with a file. Once we investigate that file, we discover that these two findings are associated with CobaltStrike. Up to here, we've followed the abnormal activity and found the malicious IP addresses. Our findings represent the C2 communication. Now let's conclude our hunt by gathering the low hanging fruits with Suricata logs.

- Query: - `event_type=="alert" | count() by alert.severity,alert.category | sort count`

![image](https://user-images.githubusercontent.com/51442719/203446210-e7918caf-5a4c-4bb8-8458-8f1ad04b4b9a.png)

Now we can see the overall malicious activities detected by Suricata. Note that you can investigate the rest of the IP addresses to identify the secondary C2 traffic anomaly without using the Suricata logs. This task demonstrates two different approaches to detecting anomalies. 

Investigating each alarm category and signature to enhance the threat hunting activities and post-hunting system hardening operations is suggested. Please note, Adversaries using CobaltStrike are usually skilled threats and don't rely on a single C2 channel. Common experience and use cases recommend digging and keeping the investigation by looking at additional C2 channels.

This concludes our hunt for the given case. Now, repeat this exercise in the attached VM and ask the questions below.

--- 

## Task 7  Exercise: Threat Hunting with Brim | Crypto Mining

--- 

## Task 8  Conclusion

**Congratulations!** You just finished the Brim room.

In this room, we covered Brim, what it is, how it operates, and how to use it to investigate threats. 

Now, we invite you to complete the Brim challenge room: Masterminds

---
---

- [Brim TryHackMe](https://medium.com/@WriteupsTHM_HTB_CTF/brim-tryhackme-28f7da657419)
