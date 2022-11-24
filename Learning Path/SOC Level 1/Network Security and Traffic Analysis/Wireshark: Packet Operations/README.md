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

### IPv4 and IPv6

Up to here, almost all options provided information that contained both versions of the IP addresses. The statistics menu has two options for narrowing the statistics on packets containing a specific IP version. Thus, analysts can identify and list all events linked to specific IP versions in a single window and use it for the event of interest. You can use the "Statistics --> IPvX Statistics" menu to view this info.

![image](https://user-images.githubusercontent.com/51442719/203675825-adf4a3e4-f781-4af9-88fd-0c4acd770dc3.png)

### DNS
This option breaks down all DNS packets from the capture file and helps analysts view the findings in a tree view based on packet counters and percentages of the DNS protocol. Thus analysts can view the DNS service's overall usage, including rcode, opcode, class, query type, service and query stats and use it for the event of interest. You can use the "Statistics --> DNS" menu to view this info.

![image](https://user-images.githubusercontent.com/51442719/203675852-3a636be6-2e1c-47b1-b3db-a62e5b531fef.png)

### HTTP
This option breaks down all HTTP packets from the capture file and helps analysts view the findings in a tree view based on packet counters and percentages of the HTTP protocol. Thus analysts can view the HTTP service's overall usage, including request and response codes and the original requests. You can use the "Statistics --> HTTP" menu to view this info.

![image](https://user-images.githubusercontent.com/51442719/203675882-029dc9af-c656-4569-beb8-0119ca27ae2e.png)

---

## Task 4  Packet Filtering | Principles

### Packet Filtering

In the previous room ([Wireshark | The Basics](https://tryhackme.com/room/wiresharkthebasics)), we covered packet filtering and how to filter packets without using queries. In this room, we will use queries to filter packets. As mentioned earlier, there are two types of filters in Wireshark. While both use similar syntax, they are used for different purposes. Let's remember the difference between these two categories.

| Capture Filters | This type of filter is used to save only a specific part of the traffic. It is set before capturing traffic and not changeable during the capture.  |
|:---:|---|
| Display Filters | This type of filter is used to investigate packets by reducing the number of visible packets, and it is changeable during the capture.  |

> `Note`: You cannot use the display filter expressions for capturing traffic and vice versa.

The typical use case is capturing everything and filtering the packets according to the event of interest. Only experienced professionals use capture filters and sniff traffic. This is why Wireshark supports more protocol types in display filters. Please ensure you thoroughly learn how to use capture filters before using them in a live environment. Remember, you cannot capture the event of interest if your capture filter is not matching the specific traffic pattern you are looking for.

Capture Filter Syntax

These filters use byte offsets hex values and masks with boolean operators, and it is not easy to understand/predict the filter's purpose at first glance. The base syntax is explained below:

- Scope: host, net, port and portrange.
- Direction: src, dst, src or dst, src and dst,
- Protocol: ether, wlan, ip, ip6, arp, rarp, tcp and udp.
- Sample filter to capture port 80 traffic: `tcp port 80`

You can read more on capture filter syntax from [here](https://www.wireshark.org/docs/man-pages/pcap-filter.html) and [here](https://gitlab.com/wireshark/wireshark/-/wikis/CaptureFilters#useful-filters). A quick reference is available under the "Capture --> Capture Filters" menu.

![image](https://user-images.githubusercontent.com/51442719/203676174-54d25674-e83a-4cfb-9914-9ab987a36334.png)

### Display Filter Syntax

This is Wireshark's most powerful feature. It supports 3000 protocols and allows conducting packet-level searches under the protocol breakdown. The official "[Display Filter Reference](https://www.wireshark.org/docs/dfref/)" provides all supported protocols breakdown for filtering.

- Sample filter to capture port 80 traffic: `tcp.port == 80`

Wireshark has a built-in option (Display Filter Expression) that stores all supported protocol structures to help analysts create display filters. We will cover the "Display Filter Expression" menu later. Now let's understand the fundamentals of the display filter operations. A quick reference is available under the "Analyse --> Display Filters" menu.\

![image](https://user-images.githubusercontent.com/51442719/203676257-32f3ea93-b089-4a5e-bfb7-56a3d19deb1f.png)

### Comparison Operators

You can create display filters by using different comparison operators to find the event of interest. The primary operators are shown in the table below.


| English | C-Like | Description | Example |
|:---:|:---:|:---:|:---:|
| eq | == | Equal | ip.src == 10.10.10.100 |
| ne | != | Not equal | ip.src != 10.10.10.100 |
| gt | > | Greater than | ip.ttl > 250 |
| lt | < | Less Than | ip.ttl < 10 |
| ge | >= | Greater than or equal to | ip.ttl >= 0xFA |
| le | <= | Less than or equal to | ip.ttl <= 0xA |

> `Note`: Wireshark supports decimal and hexadecimal values in filtering. You can use any format you want according to the search you will conduct.

### Logical Expressions
Wireshark supports boolean syntax. You can create display filters by using logical operators as well.

<table>
<thead>
  <tr>
    <th>English  </th>
    <th>C-Like</th>
    <th>Description  </th>
    <th>Example</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>and</td>
    <td>&amp;&amp;</td>
    <td>Logical AND</td>
    <td>(ip.src == 10.10.10.100) AND (ip.src == 10.10.10.111)</td>
  </tr>
  <tr>
    <td>or</td>
    <td>||</td>
    <td>Logical OR</td>
    <td>(ip.src == 10.10.10.100) OR (ip.src == 10.10.10.111)</td>
  </tr>
  <tr>
    <td>not</td>
    <td>!</td>
    <td>Logical NOT</td>
    <td>!(ip.src == 10.10.10.222)<br>Note: Usage of !=value is deprecated; using it could provide inconsistent results. Using the !(value) style is suggested for more consistent results.</td>
  </tr>
</tbody>
</table>

Packet Filter Toolbar

The filter toolbar is where you create and apply your display filters. It is a smart toolbar that helps you create valid display filters with ease. Before starting to filter packets, here are a few tips:

- Packet filters are defined in lowercase.
- Packet filters have an autocomplete feature to break down protocol details, and each detail is represented by a "dot".
- Packet filters have a three-colour representation explained below.

| Green | Valid filter |
|:---:|---|
| Red | Invalid filter |
| Yellow | Warning filter. This filter works, but it is unreliable, and it is suggested to change it with a valid filter. |

![image](https://user-images.githubusercontent.com/51442719/203677155-5b6d0c71-a6ca-44c7-b2fb-eed302034966.png)

Filter toolbar features are shown below.

![image](https://user-images.githubusercontent.com/51442719/203677177-b976069b-e6f9-4086-a75f-ff627e0dd18e.png)

We've covered lots of principles and syntax. Let's put these into practice and start filtering packets in the next task.

---

## Task 5  Packet Filtering | Protocol Filters

### Protocol Filters

As mentioned in the previous task, Wireshark supports 3000 protocols and allows packet-level investigation by filtering the protocol fields. This task shows the creation and usage of filters against different protocol fields. 

### IP Filters

IP filters help analysts filter the traffic according to the IP level information from the packets (Network layer of the OSI model). This is one of the most commonly used filters in Wireshark. These filters filter network-level information like IP addresses, version, time to live, type of service, flags, and checksum values.

The common filters are shown in the given table.

| Filter | Description |
|:---:|:---:|
| ip | Show all IP packets. |
| ip.addr == 10.10.10.111 | Show all packets containing IP address 10.10.10.111. |
| ip.addr == 10.10.10.0/24 | Show all packets containing IP addresses from 10.10.10.0/24 subnet. |
| ip.src == 10.10.10.111 | Show all packets originated from 10.10.10.111 |
| ip.dst == 10.10.10.111 | Show all packets sent to 10.10.10.111 |
| ip.addr vs ip.src/ip.dst | Note: The ip.addr filters the traffic without considering the packet direction. The ip.src/ip.dst filters the packet depending on the packet direction. |

![image](https://user-images.githubusercontent.com/51442719/203679114-c6e890d8-6eef-4c9a-b817-81908ca0b84f.png)

### TCP and UDP Filters
TCP filters help analysts filter the traffic according to protocol-level information from the packets (Transport layer of the OSI model). These filters filter transport protocol level information like source and destination ports, sequence number, acknowledgement number, windows size, timestamps, flags, length and protocol errors.

| Filter | Description | Filter | Expression |
|:---:|:---:|:---:|:---:|
| tcp.port == 80 | Show all TCP packets with port 80  | udp.port == 53 | Show all UDP packets with port 53 |
| tcp.srcport == 1234 | Show all TCP packets originating from port 1234 | udp.srcport == 1234 | Show all UDP packets originating from port 1234 |
| tcp.dstport == 80 | Show all TCP packets sent to port 80 | udp.dstport == 5353 | Show all UDP packets sent to port 5353 |

![image](https://user-images.githubusercontent.com/51442719/203679220-42aadf55-ec90-457f-bcf4-c550cacdfc9f.png)

### Application Level Protocol Filters | HTTP and DNS
Application-level protocol filters help analysts filter the traffic according to application protocol level information from the packets (Application layer of the OSI model ). These filters filter application-specific information, like payload and linked data, depending on the protocol type.

| Filter | Description | Filter | Description |
|:---:|:---:|:---:|:---:|
| http | Show all HTTP packets | dns | Show all DNS packets |
| http.response.code == 200 | Show all packets with HTTP response code "200" | dns.flags.response == 0 | Show all DNS requests |
| http.request.method == "GET" | Show all HTTP GET requests | dns.flags.response == 1 | Show all DNS responses |
| http.request.method == "POST" | Show all HTTP POST requests | dns.qry.type == 1 | Show all DNS "A" records |

![image](https://user-images.githubusercontent.com/51442719/203679322-fadf5fc5-8c04-42e1-ba22-0b96efb1c503.png)

### Display Filter Expressions

As mentioned earlier, Wireshark has a built-in option (Display Filter Expression) that stores all supported protocol structures to help analysts create display filters. When an analyst can't recall the required filter for a specific protocol or is unsure about the assignable values for a filter, the Display Filter Expressions menu provides an easy-to-use display filter builder guide. It is available under the "Analyse --> Display Filter Expression" menu.

It is impossible to memorise all details of the display filters for each protocol. Each protocol can have different fields and can accept various types of values. The Display Filter Expressions menu shows all protocol fields, accepted value types (integer or string) and predefined values (if any). Note that it will take time and require practice to master creating filters and learning the protocol filter fields.

![image](https://user-images.githubusercontent.com/51442719/203679374-528ecf9d-efd9-43ba-94b5-79216f0bfa4a.png)

> `Note`: The first room introduced the "Colouring Rules" (Task-2). Now you know how to create display filters and filter the event of interest. You can use the "View --> Coloring Rules" menu to assign colours to highlight your display filter results.

---

## Task 6  Advanced Filtering

### Advanced Filtering

So far, you have learned the basics of packet filtering operations. Now it is time to focus on specific packet details for the event of interest. Besides the operators and expressions covered in the previous room, Wireshark has advanced operators and functions. These advanced filtering options help the analyst conduct an in-depth analysis of an event of interest.

### Filter: "contains"

| Filter | contains |
|:---:|:---:|
| Type | Comparison Operator |
| Description | Search a value inside packets. It is case-sensitive and provides similar functionality to the "Find" option by focusing on a specific field. |
| Example | Find all "Apache" servers. |
| Workflow | List all HTTP packets where packets' "server" field contains the "Apache" keyword. |
| Usage | http.server contains "Apache" |

![image](https://user-images.githubusercontent.com/51442719/203679600-bde6bbe2-c196-48d5-9a55-0839bda35456.png)

### Filter: "matches"

| Filter | matches |
|:---:|:---:|
| Type | Comparison Operator |
| Description | Search a pattern of a regular expression. It is case insensitive, and complex queries have a margin of error. |
| Example | Find all .php and .html pages. |
| Workflow | List all HTTP packets where packets' "host" fields match keywords ".php" or ".html". |
| Usage | http.host matches "\.(php\|html)" |

![image](https://user-images.githubusercontent.com/51442719/203679641-7577c7ae-458c-402a-8e39-5447828fc99e.png)

### Filter: "in"

| Filter | in |
|:---:|:---:|
| Type |  Set Membership |
| Description | Search a value or field inside of a specific scope/range. |
| Example | Find all packets that use ports 80, 443 or 8080. |
| Workflow | List all TCP packets where packets' "port" fields have values 80, 443 or 8080. |
| Usage | tcp.port in {80 443 8080} |

![image](https://user-images.githubusercontent.com/51442719/203679696-6d699c92-76c6-4215-94a8-6a71bc1372a9.png)

### Filter: "upper"

| Filter | upper |
|:---:|:---:|
| Type | Function |
| Description | Convert a string value to uppercase. |
| Example | Find all "APACHE" servers. |
| Workflow | Convert all HTTP packets' "server" fields to uppercase and list packets that contain the "APACHE" keyword. |
| Usage | upper(http.server) contains "APACHE" |

![image](https://user-images.githubusercontent.com/51442719/203679750-9c041dd5-c179-4925-a9f1-c65f56f7d539.png)

### Filter: "lower"

| Filter | lower |
|:---:|:---:|
| Type | Function |
| Description | Convert a string value to lowercase. |
| Example | Find all "apache" servers. |
| Workflow | Convert all HTTP packets' "server" fields info to lowercase and list packets that contain the "apache" keyword. |
| Usage | lower(http.server) contains "apache" |

![image](https://user-images.githubusercontent.com/51442719/203679798-2b695633-ce60-448b-a74f-5f4b5e0ec062.png)

### Filter: "string"

| Filter | string |
|:---:|:---:|
| Type | Function |
| Description | Convert a non-string value to a string. |
| Example | Find all frames with odd numbers. |
| Workflow | Convert all "frame number" fields to string values, and list frames end with odd values. |
| Usage | string(frame.number) matches "[13579]$" |

![image](https://user-images.githubusercontent.com/51442719/203679836-50ad6a75-7ded-4a5d-8ca7-3ca5ef578b77.png)

### Bookmarks and Filtering Buttons

We've covered different types of filtering options, operators and functions. It is time to create filters and save them as bookmarks and buttons for later usage. As mentioned in the previous task, the filter toolbar has a filter bookmark section to save user-created filters, which helps analysts re-use favourite/complex filters with a couple of clicks. Similar to bookmarks, you can create filter buttons ready to apply with a single click. 

Creating and using bookmarks.

![image](https://user-images.githubusercontent.com/51442719/203679857-d04a7cfa-43dc-41fe-87da-0c7c4f118ab2.png)

Creating and using display filter buttons.

![image](https://user-images.githubusercontent.com/51442719/203679883-619d9df1-93cd-49e2-a7f9-2939a18104e9.png)

### Profiles
Wireshark is a multifunctional tool that helps analysts to accomplish in-depth packet analysis. As we covered during the room, multiple preferences need to be configured to analyse a specific event of interest. It is cumbersome to re-change the configuration for each investigation case, which requires a different set of colouring rules and filtering buttons. This is where Wireshark profiles come into play. You can create multiple profiles for different investigation cases and use them accordingly. You can use the "Edit --> Configuration Profiles" menu or the "lower right bottom of the status bar --> Profile" section to create, modify and change the profile configuration.

![image](https://user-images.githubusercontent.com/51442719/203679914-74acb3db-9973-4c29-9fd3-a17f5e6e21f4.png)

---

## Task 7  Conclusion

Congratulations! 

You just finished the "Wireshark: Packet Operations" room. In this room, we covered Wireshark statistics, filters, operators and functions. 

Want to learn more? We invite you to complete the [Wireshark: Traffic Analysis room](https://tryhackme.com/jr/wiresharktrafficanalysis) to improve your Wireshark skills by investigating suspicious traffic activities. 

---
---
- [TryHackMe | Wireshark: Packet Operations Writeup](https://medium.com/@CarsonS/tryhackme-wireshark-packet-operations-writeup-30b130ee1f06)

