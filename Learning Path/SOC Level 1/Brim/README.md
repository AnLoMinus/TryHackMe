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

--- 

## Task 5  Use Cases

--- 

## Task 6  Exercise: Threat Hunting with Brim | Malware C2 Detection

--- 

## Task 7  Exercise: Threat Hunting with Brim | Crypto Mining

--- 

## Task 8  Conclusion


