![image](https://user-images.githubusercontent.com/51442719/203669880-ba98b2f8-9899-4400-be93-d866779514a0.png)

# [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations)

![image](https://user-images.githubusercontent.com/51442719/203669870-22839084-f2ed-4afd-9c88-63a0fcda1868.png)

### Learn the fundamentals of packet analysis with Wireshark and how to find the needle in the haystack!

---

- [Task 1  Introduction]()
- [Task 2  Statistics | Summary]()
- [Task 3  Statistics | Protocol Details]()
- [Task 4  Packet Filtering | Principles]()
- [Task 5  Packet Filtering | Protocol Filters]()
- [Task 6  Advanced Filtering]()
- [Task 7  Conclusion]()

---

## Task 1  Introduction

In this room, we will cover the fundamentals of packet analysis with Wireshark and investigate the event of interest at the packet-level. Note that this is the second room of the Wireshark room trio, and it is suggested to visit the first room ([Wireshark: The Basics](https://tryhackme.com/room/wiresharkthebasics)) to practice and refresh your Wireshark skills before starting this one.

In the first room, we covered the basics of the Wireshark by focusing on how it operates and how to use it to investigate traffic captures. In this room, we will cover advanced features of the Wireshark by focusing on packet-level details with Wireshark statistics, filters, operators and functions.

Note: A VM is attached to this room. You don't need SSH or RDP; the room provides a "Split View" feature. Access to the machine will be provided in-browser and will deploy in Split View mode in your browser. If you don't see it, use the blue Show Split View button at the top right of this room page to show it. DO NOT directly interact with any domains and IP addresses in this room. The domains and IP addresses are included for reference reasons only.

---

## Task 2  Statistics | Summary

### Statistics

This menu provides multiple statistics options ready to investigate to help users see the big picture in terms of the scope of the traffic, available protocols, endpoints and conversations, and some protocol-specific details like DHCP, DNS and HTTP/2. For a security analyst, it is crucial to know how to utilise the statical information. This section provides a quick summary of the processed pcap, which will help analysts create a hypothesis for an investigation. You can use the "Statistics" menu to view all available options. Now start the given VM, open the Wireshark, load the "Exercise.pcapng" file and go through the walkthrough.

### Resolved Addresses

This option helps analysts identify IP addresses and DNS names available in the capture file by providing the list of the resolved addresses and their hostnames. Note that the hostname information is taken from DNS answers in the capture file. Analysts can quickly identify the accessed resources by using this menu. Thus they can spot accessed resources and evaluate them according to the event of interest. You can use the "Statistics --> Resolved Addresses" menu to view all resolved addresses by Wireshark.

![image](https://user-images.githubusercontent.com/51442719/203673119-74084340-559c-4770-938b-b15a7d582e34.png)

### Protocol Hierarchy

This option breaks down all available protocols from the capture file and helps analysts view the protocols in a tree view based on packet counters and percentages. Thus analysts can view the overall usage of the ports and services and focus on the event of interest. The golden rule mentioned in the previous room is valid in this section; you can right-click and filter the event of interest. You can use the "Statistics --> Protocol Hierarchy" menu to view this info.

![image](https://user-images.githubusercontent.com/51442719/203673148-9df055cd-8f1d-4c80-875d-88e741eefe53.png)

### Conversations

Conversation represents traffic between two specific endpoints. This option provides the list of the conversations in five base formats; ethernet, IPv4, IPv6, TCP and UDP. Thus analysts can identify all conversations and contact endpoints for the event of interest. You can use the "Statistic --> Conversations" menu to view this info.

![image](https://user-images.githubusercontent.com/51442719/203673180-89243719-f0a2-430e-b046-d2548b10b129.png)

### Endpoints

The endpoints option is similar to the conversations option. The only difference is that this option provides unique information for a single information field (Ethernet, IPv4, IPv6, TCP and UDP ). Thus analysts can identify the unique endpoints in the capture file and use it for the event of interest. You can use the "Statistics --> Endpoints" menu to view this info.

Wireshark also supports resolving MAC addresses to human-readable format using the manufacturer name assigned by IEEE. Note that this conversion is done through the first three bytes of the MAC address and only works for the known manufacturers. When you review the ethernet endpoints, you can activate this option with the "Name resolution" button in the lower-left corner of the endpoints window.

![image](https://user-images.githubusercontent.com/51442719/203673208-103ad76f-d345-4bd5-8cff-fdc4c8b88e5c.png)

Name resolution is not limited only to MAC addresses. Wireshark provides IP and port name resolution options as well. However, these options are not enabled by default. If you want to use these functionalities, you need to activate them through the "Edit --> Preferences --> Name Resolution" menu. Once you enable IP and port name resolution, you will see the resolved IP address and port names in the packet list pane and also will be able to view resolved names in the "Conversations" and "Endpoints" menus as well.

![image](https://user-images.githubusercontent.com/51442719/203673231-59ea89a8-e0dc-4da6-abe9-ae266d194624.png)

Endpoint menu view with name resolution:

![image](https://user-images.githubusercontent.com/51442719/203673253-61c0f968-d7b2-43d2-a63e-e34727290b85.png)

Besides name resolution, Wireshark also provides an IP geolocation mapping that helps analysts identify the map's source and destination addresses. But this feature is not activated by default and needs supplementary data like the GeoIP database. Currently, Wireshark supports MaxMind databases, and the latest versions of the Wireshark come configured MaxMind DB resolver. However, you still need MaxMind DB files and provide the database path to Wireshark by using the "Edit --> Preferences --> Name Resolution --> MaxMind database directories" menu. Once you download and indicate the path, Wireshark will automatically provide GeoIP information under the IP protocol details for the matched IP addresses.

![image](https://user-images.githubusercontent.com/51442719/203673296-1d64af2b-257d-438a-ba9f-abf8cc6682c1.png)

Endpoints and GeoIP view.

![image](https://user-images.githubusercontent.com/51442719/203673324-a6647bf4-d664-445f-bf3f-507c3e3d16ad.png)

> `Note`: You need an active internet connection to view the GeoIP map. The lab machine doesn't have an active internet connection!


---

## Task 3  Statistics | Protocol Details

---

## Task 4  Packet Filtering | Principles

---

## Task 5  Packet Filtering | Protocol Filters

---

## Task 6  Advanced Filtering

---

## Task 7  Conclusion
