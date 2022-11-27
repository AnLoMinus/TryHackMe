![image](https://user-images.githubusercontent.com/51442719/203683087-b01e9e65-a5d5-4c38-ba25-3081d2aba280.png)

# [Wireshark: Traffic Analysis](https://tryhackme.com/room/wiresharktrafficanalysis)

![image](https://user-images.githubusercontent.com/51442719/203683070-2b8e4ff0-a827-44f6-b761-079be4941779.png)

### Learn the basics of traffic analysis with Wireshark and how to find anomalies on your network!

---

- [Task 1  Introduction](#)
- [Task 2  Nmap Scans](#)
- [Task 3  ARP Poisoning & Man In The Middle!](#)
- [Task 4  Identifying Hosts: DHCP, NetBIOS and Kerberos](#)
- [Task 5  Tunneling Traffic: DNS and ICMP](#)
- [Task 6  Cleartext Protocol Analysis: FTP](#)
- [Task 7  Cleartext Protocol Analysis: HTTP](#)
- [Task 8  Encrypted Protocol Analysis: Decrypting HTTPS](#)
- [Task 9  Bonus: Hunt Cleartext Credentials!](#)
- [Task 10  Bonus: Actionable Results!](#)
- [Task 11  Conclusion](#)

---

## Task 1  Introduction

In this room, we will cover the techniques and key points of traffic analysis with Wireshark and detect suspicious activities. Note that this is the third and last room of the Wireshark room trio, and it is suggested to visit the first two rooms stated below to practice and refresh your Wireshark skills before starting this one.

- [Wireshark: The Basics](https://tryhackme.com/room/wiresharkthebasics)
- [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations)

In the first two rooms, we have covered how to use Wireshark and do packet-level searches. Now, it is time to investigate and correlate the packet-level information to see the big picture in the network traffic, like detecting anomalies and malicious activities. For a security analyst, it is vital to stop and understand pieces of information spread in packets by applying the analyst's knowledge and tool functionality. This room will cover investigating packet-level details by synthesising the analyst knowledge and  Wireshark functionality for detecting anomalies and odd situations for a given case.

Note: A VM is attached to this room. You don't need SSH or RDP; the room provides a "Split View" feature. DO NOT directly interact with any domains and IP addresses in this room. The domains and IP addresses are included only for reference reasons.


---

## Task 2  Nmap Scans

### Nmap Scans

Nmap is an industry-standard tool for mapping networks, identifying live hosts and discovering the services. As it is one of the most used network scanner tools, a security analyst should identify the network patterns created with it. This section will cover identifying the most common Nmap scan types.

- TCP connect scans
- SYN scans
- UDP scans

It is essential to know how Nmap scans work to spot scan activity on the network. However, it is impossible to understand the scan details without using the correct filters. Below are the base filters to probe Nmap scan behaviour on the network. 

TCP flags in a nutshell.

- `Synchronization` (`SYN`) 
  – It is used in first step of connection establishment phase or 3-way handshake process between the two hosts. Only the first packet from sender as well as receiver should have this flag set. This is used for synchronizing sequence number i.e. to tell the other end which sequence number they should accept.

- `Acknowledgement` (`ACK`)
  - It is used to acknowledge packets which are successful received by the host. The flag is set if the acknowledgement number field contains a valid acknowledgement number. 
In given below diagram, the receiver sends an ACK = 1 as well as SYN = 1 in the second step of connection establishment to tell sender that it received its initial packet. 
 
- `Finish` (`FIN`) 
  - It is used to request for connection termination i.e. when there is no more data from the sender, it requests for connection termination. This is the last packet sent by sender. It frees the reserved resources and gracefully terminate the connection. 
 
- `Reset` (`RST`) 
  - It is used to terminate the connection if the RST sender feels something is wrong with the TCP connection or that the conversation should not exist. It can get send from receiver side when packet is send to particular host that was not expecting it. 

- `Push` (`PSH`) 
  - Transport layer by default waits for some time for application layer to send enough data equal to maximum segment size so that the number of packets transmitted on network minimizes which is not desirable by some application like interactive applications(chatting). Similarly transport layer at receiver end buffers packets and transmit to application layer if it meets certain criteria. 
This problem is solved by using PSH. Transport layer sets PSH = 1 and immediately sends the segment to network layer as soon as it receives signal from application layer. Receiver transport layer, on seeing PSH = 1 immediately forwards the data to application layer. 
In general, it tells the receiver to process these packets as they are received instead of buffering them. 
 
- `Urgent` (`URG`) 
  - Data inside a segment with URG = 1 flag is forwarded to application layer immediately even if there are more data to be given to application layer. It is used to notify the receiver to process the urgent packets before processing all other packets. The receiver will be notified when all known urgent data has been received.


<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Wireshark Filters</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Global search.</td>
    <td>tcp<br>udp</td>
  </tr>
  <tr>
    <td>Only SYN flag.<br>SYN flag is set. The rest of the bits are not important.</td>
    <td>tcp.flags == 2<br>tcp.flags.syn == 1</td>
  </tr>
  <tr>
    <td>Only ACK flag.<br>ACK flag is set. The rest of the bits are not important.<br></td>
    <td>tcp.flags == 16<br>tcp.flags.ack == 1</td>
  </tr>
  <tr>
    <td>Only SYN, ACK flags.<br>SYN and ACK are set. The rest of the bits are not important.</td>
    <td>tcp.flags == 18<br>(tcp.flags.syn == 1) and (tcp.flags.ack == 1)</td>
  </tr>
  <tr>
    <td>Only RST flag.<br>RST flag is set. The rest of the bits are not important.<br></td>
    <td><br>tcp.flags == 4<br>tcp.flags.reset == 1</td>
  </tr>
  <tr>
    <td>Only RST, ACK flags.<br>RST and ACK are set. The rest of the bits are not important.<br></td>
    <td>tcp.flags == 20<br>(tcp.flags.reset == 1) and (tcp.flags.ack == 1)</td>
  </tr>
  <tr>
    <td>Only FIN flag<br>FIN flag is set. The rest of the bits are not important.</td>
    <td>tcp.flags == 1<br>tcp.flags.fin == 1</td>
  </tr>
</tbody>
</table>

### TCP Connect Scans

TCP Connect Scan in a nutshell:

- Relies on the three-way handshake (needs to finish the handshake process).
- Usually conducted with `nmap -sT` command.
- Used by non-privileged users (only option for a non-root user).
- Usually has a windows size larger than 1024 bytes as the request expects some data due to the nature of the protocol.

The images below show the three-way handshake process of the open and close TCP ports. Images and pcap samples are split to make the investigation easier and understand each case's details.

Open TCP port (Connect):

![image](https://user-images.githubusercontent.com/51442719/203868119-43dd60fa-72ed-4d12-a643-cac295140558.png)

Closed TCP port (Connect):

![image](https://user-images.githubusercontent.com/51442719/203868136-b158d2b2-f671-43d4-b680-7edaa7f9892b.png)

The above images provide the patterns in isolated traffic. However, it is not always easy to spot the given patterns in big capture files. Therefore analysts need to use a generic filter to view the initial anomaly patterns, and then it will be easier to focus on a specific traffic point. The given filter shows the TCP Connect scan patterns in a capture file.

- `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024 `

![image](https://user-images.githubusercontent.com/51442719/203868154-6b56e2f8-d8bc-4aaf-8b81-8b15ec5e3216.png)


### SYN Scans

TCP SYN Scan in a nutshell:

- Doesn't rely on the three-way handshake (no need to finish the handshake process).
- Usually conducted with `nmap -sS` command.
- Used by privileged users.
- Usually have a size less than or equal to 1024 bytes as the request is not finished and it doesn't expect to receive data.

Open TCP port (SYN):

![image](https://user-images.githubusercontent.com/51442719/203868239-86f5a65e-4d32-4fb2-b7d7-6aa4c9045981.png)

Closed TCP port (SYN):

![image](https://user-images.githubusercontent.com/51442719/203868268-cbf65735-7e63-4450-84be-c9c3eb797099.png)

The given filter shows the TCP SYN scan patterns in a capture file.

- `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024`

![image](https://user-images.githubusercontent.com/51442719/203868326-810ff65c-ecd6-4f2f-982c-ecff60221f0a.png)


### UDP Scans

UDP Scan in a nutshell:

- Doesn't require a handshake process
- No prompt for open ports
- ICMP error message for close ports
- Usually conducted with `nmap -sU` command.

Closed (port no 69) and open (port no 68) UDP ports:

![image](https://user-images.githubusercontent.com/51442719/203868339-a1e2d08c-14e6-47a6-83a5-fdaa7e312197.png)

The above image shows that the closed port returns an ICMP error packet. No further information is provided about the error at first glance, so how can an analyst decide where this error message belongs? The ICMP error message uses the original request as encapsulated data to show the source/reason of the packet. Once you expand the ICMP section in the packet details pane, you will see the encapsulated data and the original request, as shown in the below image.


![image](https://user-images.githubusercontent.com/51442719/203868361-c3e60385-65a8-4874-b36c-3f78f4f105a8.png)

The given filter shows the UDP scan patterns in a capture file.

- `icmp.type==3 and icmp.code==3`

![image](https://user-images.githubusercontent.com/51442719/203881339-97261194-3d49-4420-af9f-3180dd7841a4.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!

---

## Task 3  ARP Poisoning & Man In The Middle!

### ARP Poisoning/Spoofing (A.K.A. Man In The Middle Attack)

ARP protocol, or Address Resolution Protocol (ARP), is the technology responsible for allowing devices to identify themselves on a network. Address Resolution Protocol Poisoning (also known as ARP Spoofing or Man In The Middle (MITM) attack) is a type of attack that involves network jamming/manipulating by sending malicious ARP packets to the default gateway. The ultimate aim is to manipulate the "IP to MAC address table" and sniff the traffic of the target host.

There are a variety of tools available to conduct ARP attacks. However, the mindset of the attack is static, so it is easy to detect such an attack by knowing the ARP protocol workflow and Wireshark skills.    

#### ARP analysis in a nutshell:

- Works on the local network
- Enables the communication between MAC addresses
- Not a secure protocol
- Not a routable protocol
- It doesn't have an authentication function
- Common patterns are request & response, announcement and gratuitous packets.

Before investigating the traffic, let's review some legitimate and suspicious ARP packets. The legitimate requests are similar to the shown picture: a broadcast request that asks if any of the available hosts use an IP address and a reply from the host that uses the particular IP address.

<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Wireshark filter</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Global search</td>
    <td>arp</td>
  </tr>
  <tr>
    <td>"ARP" options for grabbing the low-hanging fruits:<br>Opcode 1: ARP requests.<br>Opcode 2: ARP responses.<br>Hunt: Arp scanning<br>Hunt: Possible ARP poisoning detection<br>Hunt: Possible ARP flooding from detection:</td>
    <td>arp.opcode == 1<br>arp.opcode == 2<br>arp.dst.hw_mac==00:00:00:00:00:00<br>arp.duplicate-address-detected or arp.duplicate-address-frame<br>((arp) &amp;&amp; (arp.opcode == 1)) &amp;&amp; (arp.src.hw_mac == target-mac-address)<br></td>
  </tr>
</tbody>
</table>

![image](https://user-images.githubusercontent.com/51442719/203881582-01eef49a-c994-4578-ad3f-e2440d91eaa7.png)

A suspicious situation means having two different ARP responses (conflict) for a particular IP address. In that case, Wireshark's expert info tab warns the analyst. However, it only shows the second occurrence of the duplicate value to highlight the conflict. Therefore, identifying the malicious packet from the legitimate one is the analyst's challenge. A possible IP spoofing case is shown in the picture below.

![image](https://user-images.githubusercontent.com/51442719/203881594-8475ec59-cd8b-4829-a71d-eb723e446dc9.png)

Here, knowing the network architecture and inspecting the traffic for a specific time frame can help detect the anomaly. As an analyst, you should take notes of your findings before going further. This will help you be organised and make it easier to correlate the further findings. Look at the given picture; there is a conflict; the MAC address that ends with "b4" crafted an ARP request with the "192.168.1.25" IP address, then claimed to have the "192.168.1.1" IP address.


<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Detection Notes<br></th>
    <th>Findings</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Possible IP address match.<br></td>
    <td>1 IP address announced from a MAC address.<br></td>
    <td>MAC: 00:0c:29:e2:18:b4<br>IP: 192.168.1.25</td>
  </tr>
  <tr>
    <td>Possible ARP spoofing attempt.<br></td>
    <td>2 MAC addresses claimed the same IP address (192.168.1.1).<br>The " 192.168.1.1" IP address is a possible gateway address.<br></td>
    <td>MAC1: 50:78:b3:f3:cd:f4<br>MAC 2: 00:0c:29:e2:18:b4</td>
  </tr>
  <tr>
    <td>Possible ARP flooding attempt.<br></td>
    <td>The MAC address that ends with "b4" claims to have a different/new IP address.<br></td>
    <td>MAC: 00:0c:29:e2:18:b4<br>IP: 192.168.1.1</td>
  </tr>
</tbody>
</table>

Let's keep inspecting the traffic to spot any other anomalies. Note that the case is split into multiple capture files to make the investigation easier.

![image](https://user-images.githubusercontent.com/51442719/203881631-4c49eaca-55aa-47c4-ab50-254db951c70d.png)

At this point, it is evident that there is an anomaly. A security analyst cannot ignore a flood of ARP requests. This could be malicious activity, scan or network problems. There is a new anomaly; the MAC address that ends with "b4" crafted multiple ARP requests with the "192.168.1.25" IP address. Let's focus on the source of this anomaly and extend the taken notes. 

<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Detection Notes</th>
    <th>Findings</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Possible IP address match.<br></td>
    <td>1 IP address announced from a MAC address.<br></td>
    <td><br>MAC: 00:0c:29:e2:18:b4<br>IP: 192.168.1.25<br></td>
  </tr>
  <tr>
    <td>Possible ARP spoofing attempt.<br></td>
    <td><br>2 MAC addresses claimed the same IP address (192.168.1.1).The " 192.168.1.1" IP address is a possible gateway address.<br></td>
    <td>MAC1: 50:78:b3:f3:cd:f4<br>MAC 2: 00:0c:29:e2:18:b4</td>
  </tr>
  <tr>
    <td>Possible ARP spoofing attempt.<br></td>
    <td>The MAC address that ends with "b4" claims to have a different/new IP address.<br></td>
    <td>MAC: 00:0c:29:e2:18:b4<br>IP: 192.168.1.1</td>
  </tr>
  <tr>
    <td>Possible ARP flooding attempt.<br></td>
    <td>The MAC address that ends with "b4" crafted multiple ARP requests against a range of IP addresses.</td>
    <td>MAC: 00:0c:29:e2:18:b4<br>IP: 192.168.1.xxx</td>
  </tr>
</tbody>
</table>

Up to this point, it is evident that the MAC address that ends with "b4" owns the "192.168.1.25" IP address and crafted suspicious ARP requests against a range of IP addresses. It also claimed to have the possible gateway address as well. Let's focus on other protocols and spot the reflection of this anomaly in the following sections of the time frame. 

![image](https://user-images.githubusercontent.com/51442719/203881679-1c39a56c-9978-445a-a1d3-ae761913bceb.png)

There is HTTP traffic, and everything looks normal at the IP level, so there is no linked information with our previous findings. Let's add the MAC addresses as columns in the packet list pane to reveal the communication behind the IP addresses.

![image](https://user-images.githubusercontent.com/51442719/203881722-bfcc2b9b-518d-4b46-a5ae-8ae31f379dee.png)

One more anomaly! The MAC address that ends with "b4" is the destination of all HTTP packets! It is evident that there is a MITM attack, and the attacker is the host with the MAC address that ends with "b4". All traffic linked to "192.168.1.12" IP addresses is forwarded to the malicious host. Let's summarise the findings before concluding the investigation.  

<table>
<thead>
  <tr>
    <th>Detection Notes</th>
    <th>Findings</th>
    <th></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>IP to MAC matches.</td>
    <td>3  IP to MAC address matches. </td>
    <td><br>MAC: 00:0c:29:e2:18:b4 = IP: 192.168.1.25<br>MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.1<br>MAC: 00:0c:29:98:c7:a8 = IP: 192.168.1.12<br></td>
  </tr>
  <tr>
    <td>Attacker</td>
    <td>The attacker created noise with ARP packets.<br></td>
    <td>MAC: 00:0c:29:e2:18:b4 = IP: 192.168.1.25<br></td>
  </tr>
  <tr>
    <td>Router/gateway<br></td>
    <td>Gateway address.<br></td>
    <td>MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.1<br></td>
  </tr>
  <tr>
    <td>Victim<br></td>
    <td>The attacker sniffed all traffic of the victim.</td>
    <td>MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.12<br></td>
  </tr>
</tbody>
</table>

Detecting these bits and pieces of information in a big capture file is challenging. However, in real-life cases, you will not have "tailored data" ready for investigation. Therefore you need to have the analyst mindset, knowledge and tool skills to filter and detect the anomalies. 

> `Note`: In traffic analysis, there are always alternative solutions available. The solution type and the approach depend on the analyst's knowledge and skill level and the available data sources. 

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!

---

## Task 4  Identifying Hosts: DHCP, NetBIOS and Kerberos

### Identifying Hosts
When investigating a compromise or malware infection activity, a security analyst should know how to identify the hosts on the network apart from IP to MAC address match. One of the best methods is identifying the hosts and users on the network to decide the investigation's starting point and list the hosts and users associated with the malicious traffic/activity.

Usually, enterprise networks use a predefined pattern to name users and hosts. While this makes knowing and following the inventory easier, it has good and bad sides. The good side is that it will be easy to identify a user or host by looking at the name. The bad side is that it will be easy to clone that pattern and live in the enterprise network for adversaries. There are multiple solutions to avoid these kinds of activities, but for a security analyst, it is still essential to have host and user identification skills.

Protocols that can be used in Host and User identification:

- Dynamic Host Configuration Protocol (DHCP) traffic
- NetBIOS (NBNS) traffic 
- Kerberos traffic

### DHCP Analysis
DHCP protocol, or Dynamic Host Configuration Protocol (DHCP), is the technology responsible for managing automatic IP address and required communication parameters assignment.

DHCP investigation in a nutshell:

<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Wireshark Filter</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Global search.</td>
    <td>dhcp or bootp</td>
  </tr>
  <tr>
    <td>Filtering the proper DHCP packet options is vital to finding an event of interest. <br><br><br>"DHCP Request" packets contain the hostname information<br>"DHCP ACK" packets represent the accepted requests<br>"DHCP NAK" packets represent denied requests<br>Due to the nature of the protocol, only "Option 53" ( request type) has predefined static values. You should filter the packet type first, and then you can filter the rest of the options by "applying as column" or use the advanced filters like "contains" and "matches".<br></td>
    <td> <br><br> Request: dhcp.option.dhcp == 3 <br> ACK: dhcp.option.dhcp == 5 <br> NAK: dhcp.option.dhcp == 6 <br> </td>
  </tr>
  <tr>
    <td><br>"DHCP Request" options for grabbing the low-hanging fruits:<br>Option 12: Hostname.<br>Option 50: Requested IP address.<br>Option 51: Requested IP lease time.<br>Option 61: Client's MAC address.</td>
    <td>dhcp.option.hostname contains "keyword"</td>
  </tr>
  <tr>
    <td><br>"DHCP ACK" options for grabbing the low-hanging fruits:<br>Option 15: Domain name.<br>Option 51: Assigned IP lease time.</td>
    <td>dhcp.option.domain_name contains "keyword"</td>
  </tr>
  <tr>
    <td><br>"DHCP NAK" options for grabbing the low-hanging fruits:<br>Option 56: Message (rejection details/reason).</td>
    <td>As the message could be unique according to the case/situation, It is suggested to read the message instead of filtering it. Thus, the analyst could create a more reliable hypothesis/result by understanding the event circumstances.</td>
  </tr>
</tbody>
</table>

![image](https://user-images.githubusercontent.com/51442719/203883379-e5f0ba48-b4d3-4d87-8838-cae71831a945.png)

### NetBIOS (NBNS) Analysis

NetBIOS or Network Basic Input/Output System is the technology responsible for allowing applications on different hosts to communicate with each other. 

NBNS investigation in a nutshell:

<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Wireshark Filter</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Global search.</td>
    <td>nbns</td>
  </tr>
  <tr>
    <td>"NBNS" options for grabbing the low-hanging fruits:<br><br>Queries: Query details.<br>Query details could contain "name, Time to live (TTL) and IP address details"</td>
    <td>nbns.name contains "keyword"</td>
  </tr>
</tbody>
</table>

![image](https://user-images.githubusercontent.com/51442719/203883459-ff263cc9-821d-4700-bb43-4761ac97c866.png)

### Kerberos Analysis

Kerberos is the default authentication service for Microsoft Windows domains. It is responsible for authenticating service requests between two or more computers over the untrusted network. The ultimate aim is to prove identity securely.

Kerberos investigation in a nutshell:

<table>
<thead>
  <tr>
    <th>Notes</th>
    <th>Wireshark Filter</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Global search.</td>
    <td>kerberos</td>
  </tr>
  <tr>
    <td>User account search:<br>CNameString: The username.<br>Note: Some packets could provide hostname information in this field. To avoid this confusion, filter the "$" value. The values end with "$" are hostnames, and the ones without it are user names.<br></td>
    <td>kerberos.CNameString contains "keyword" <br>kerberos.CNameString and !(kerberos.CNameString contains "$" )</td>
  </tr>
  <tr>
    <td>"Kerberos" options for grabbing the low-hanging fruits:<br>pvno: Protocol version.<br>realm: Domain name for the generated ticket.<br><br>sname: Service and domain name for the generated ticket.<br>addresses: Client IP address and NetBIOS name.<br><br>Note: the "addresses" information is only available in request packets.</td>
    <td>kerberos.pvno == 5<br>kerberos.realm contains ".org" <br>kerberos.SNameString == "krbtg"</td>
  </tr>
</tbody>
</table>

![image](https://user-images.githubusercontent.com/51442719/203883506-b7bbae3b-aab1-4950-9d99-2701da5a02fb.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!

---

## Task 5  Tunneling Traffic: DNS and ICMP

### Tunnelling Traffic: ICMP and DNS 

Traffic tunnelling is (also known as "port forwarding") transferring the data/resources in a secure method to network segments and zones. It can be used for "internet to private networks" and "private networks to internet" flow/direction. There is an encapsulation process to hide the data, so the transferred data appear natural for the case, but it contains private data packets and transfers them to the final destination securely.

Tunnelling provides anonymity and traffic security. Therefore it is highly used by enterprise networks. However, as it gives a significant level of data encryption, attackers use tunnelling to bypass security perimeters using the standard and trusted protocols used in everyday traffic like ICMP and DNS. Therefore, for a security analyst, it is crucial to have the ability to spot ICMP and DNS anomalies.

### ICMP Analysis 

Internet Control Message Protocol (ICMP) is designed for diagnosing and reporting network communication issues. It is highly used in error reporting and testing. As it is a trusted network layer protocol, sometimes it is used for denial of service (DoS) attacks; also, adversaries use it in data exfiltration and C2 tunnelling activities.

#### ICMP analysis in a nutshell:

Usually, ICMP tunnelling attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. As the ICMP packets can transfer an additional data payload, adversaries use this section to exfiltrate data and establish a C2 connection. It could be a TCP, HTTP or SSH data. As the ICMP protocols provide a great opportunity to carry extra data, it also has disadvantages. Most enterprise networks block custom packets or require administrator privileges to create custom ICMP packets.

A large volume of ICMP traffic or anomalous packet sizes are indicators of ICMP tunnelling. Still, the adversaries could create custom packets that match the regular ICMP packet size (64 bytes), so it is still cumbersome to detect these tunnelling activities. However, a security analyst should know the normal and the abnormal to spot the possible anomaly and escalate it for further analysis.

| Notes | Wireshark filters |
|:---:|:---:|
| Global search | icmp |
| "ICMP" options for grabbing the low-hanging fruits: <li>Packet length. <li>ICMP destination addresses.  <li>Encapsulated protocol signs in ICMP payload. | <code>data.len > 64 and icmp</code> |

![image](https://user-images.githubusercontent.com/51442719/204114677-bef8c107-4a2b-4d7b-b086-784c4e9d66fb.png)

### DNS Analysis 

Domain Name System (DNS) is designed to translate/convert IP domain addresses to IP addresses. It is also known as a phonebook of the internet. As it is the essential part of web services, it is commonly used and trusted, and therefore often ignored. Due to that, adversaries use it in data exfiltration and C2 activities.

### DNS analysis in a nutshell:

Similar to ICMP tunnels, DNS attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. Adversary creates (or already has) a domain address and configures it as a C2 channel. The malware or the commands executed after exploitation sends DNS queries to the C2 server. However, these queries are longer than default DNS queries and crafted for subdomain addresses. Unfortunately, these subdomain addresses are not actual addresses; they are encoded commands as shown below:

"encoded-commands.maliciousdomain.com"

When this query is routed to the C2 server, the server sends the actual malicious commands to the host. As the DNS queries are a natural part of the networking activity, these packets have the chance of not being detected by network perimeters. A security analyst should know how to investigate the DNS packet lengths and target addresses to spot these anomalies. 

| Notes | Wireshark Filter |
|:---:|:---:|
| Global search | dns |
| "DNS" options for grabbing the low-hanging fruits: <li>Query length. <li>Anomalous and non-regular names in DNS addresses. <li>Long DNS addresses with encoded subdomain addresses. <li>Known patterns like dnscat and dns2tcp. <li>Statistical analysis like the anomalous volume of DNS requests for a particular target. !mdns: Disable local link device queries. | <li> dns contains "dnscat" <li>dns.qry.name.len > 15 and !mdns |

![image](https://user-images.githubusercontent.com/51442719/204114737-01bc089f-7a2f-4255-8968-53e188909fde.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!

---

## Task 6  Cleartext Protocol Analysis: FTP

### Cleartext Protocol Analysis

Investigating cleartext protocol traces sounds easy, but when the time comes to investigate a big network trace for incident analysis and response, the game changes. Proper analysis is more than following the stream and reading the cleartext data. For a security analyst, it is important to create statistics and key results from the investigation process. As mentioned earlier at the beginning of the Wireshark room series, the analyst should have the required network knowledge and tool skills to accomplish this. Let's simulate a cleartext protocol investigation with Wireshark!

### FTP Analysis 

File Transfer Protocol (FTP) is designed to transfer files with ease, so it focuses on simplicity rather than security. As a result of this, using this protocol in unsecured environments could create security issues like:

- MITM attacks
- Credential stealing and unauthorised access
- Phishing
- Malware planting
- Data exfiltration

#### FTP analysis in a nutshell:

| Notes | Wireshark Filter |
|:---:|:---:|
| Global search | ftp |
| "FTP" options for grabbing the low-hanging fruits:<br>x1x series: Information request responses.<br>x2x series: Connection messages.<br>x3x series: Authentication messages.<br>Note: "200" means command successful. | --- |
| "x1x" series options for grabbing the low-hanging fruits:<br>211: System status.<br>212: Directory status.<br>213: File status | ftp.response.code == 211  |
| "x2x" series options for grabbing the low-hanging fruits:<br>220: Service ready.<br>227: Entering passive mode.<br>228: Long passive mode.<br>229: Extended passive mode. | ftp.response.code == 227 |
| "x3x" series options for grabbing the low-hanging fruits:<br>230: User login.<br>231: User logout.<br>331: Valid username.<br>430: Invalid username or password<br>530: No login, invalid password. | ftp.response.code == 230 |
| "FTP" commands for grabbing the low-hanging fruits:<br>USER: Username.<br>PASS: Password.<br>CWD: Current work directory.<br>LIST: List. | ftp.request.command == "USER"<br>ftp.request.command == "PASS"<br>ftp.request.arg == "password" |
| Advanced usages examples for grabbing low-hanging fruits:<br>Bruteforce signal: List failed login attempts.<br>Bruteforce signal: List target username.<br>Password spray signal: List targets for a static password. | ftp.response.code == 530<br>(ftp.response.code == 530) and (ftp.response.arg contains "username")<br>(ftp.request.command == "PASS" ) and (ftp.request.arg == "password") |

![image](https://user-images.githubusercontent.com/51442719/204114809-485a15a5-fb56-4919-83d8-ec0be0b6a42b.png)
  
Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!


---

## Task 7  Cleartext Protocol Analysis: HTTP

### HTTP Analysis 

Hypertext Transfer Protocol (HTTP) is a cleartext-based, request-response and client-server protocol. It is the standard type of network activity to request/serve web pages, and by default, it is not blocked by any network perimeter. As a result of being unencrypted and the backbone of web traffic, HTTP is one of the must-to-know protocols in traffic analysis. Following attacks could be detected with the help of HTTP analysis:

- Phishing pages
- Web attacks
- Data exfiltration
- Command and control traffic (C2)

#### HTTP analysis in a nutshell:

| Notes | Wireshark Filter |
|:---:|:---:|
| Global search<br>Note: HTTP2 is a revision of the HTTP protocol for better performance and security. It supports binary data transfer and request&response multiplexing. | http<br>http2 |
| "HTTP Request Methods" for grabbing the low-hanging fruits:<br>GET<br>POST<br>Request: Listing all requests | http.request.method == "GET"<br>http.request.method == "POST"<br>http.request |
| "HTTP Response Status Codes" for grabbing the low-hanging fruits:<br>200 OK: Request successful.<br>301 Moved Permanently: Resource is moved to a new URL/path (permanently).<br>302 Moved Temporarily: Resource is moved to a new URL/path (temporarily).<br>400 Bad Request: Server didn't understand the request.<br>401 Unauthorised: URL needs authorisation (login, etc.).<br>403 Forbidden: No access to the requested URL. <br>404 Not Found: Server can't find the requested URL.<br>405 Method Not Allowed: Used method is not suitable or blocked.<br>408 Request Timeout:  Request look longer than server wait time.<br>500 Internal Server Error: Request not completed, unexpected error.<br>503 Service Unavailable: Request not completed server or service is down. | http.response.code == 200<br>http.response.code == 401<br>http.response.code == 403<br>http.response.code == 404<br>http.response.code == 405<br>http.response.code == 503 |
| "HTTP Parameters" for grabbing the low-hanging fruits:<br>User agent: Browser and operating system identification to a web server application.<br>Request URI: Points the requested resource from the server.<br><br>Full *URI: Complete URI information.<br>*URI: Uniform Resource Identifier. | http.user_agent contains "nmap"<br>http.request.uri contains "admin"<br>http.request.full_uri contains "admin" |
| "HTTP Parameters" for grabbing the low-hanging fruits:<br>Server: Server service name.<br><br>Host: Hostname of the server<br>Connection: Connection status.<br><br>Line-based text data: Cleartext data provided by the server.<br>HTML Form URL Encoded: Web form information. | http.server contains "apache"<br>http.host contains "keyword"<br>http.host == "keyword"<br>http.connection == "Keep-Alive"<br>data-text-lines contains "keyword" |  

### User Agent Analysis 

As the adversaries use sophisticated technics to accomplish attacks, they try to leave traces similar to natural traffic through the known and trusted protocols. For a security analyst, it is important to spot the anomaly signs on the bits and pieces of the packets. The "user-agent" field is one of the great resources for spotting anomalies in HTTP traffic. In some cases, adversaries successfully modify the user-agent data, which could look super natural. A security analyst cannot rely only on the user-agent field to spot an anomaly. Never whitelist a user agent, even if it looks natural. User agent-based anomaly/threat detection/hunting is an additional data source to check and is useful when there is an obvious anomaly. If you are unsure about a value, you can conduct a web search to validate your findings with the default and normal user-agent info ([example site](https://developers.whatismybrowser.com/useragents/explore/)).

#### User Agent analysis in a nutshell:

| Notes | Wireshark Filter |
|:---:|:---:|
| Global search. | http.user_agent |
| Research outcomes for grabbing the low-hanging fruits:<br>Different user agent information from the same host in a short time notice.<br>Non-standard and custom user agent info.<br>Subtle spelling differences. ("Mozilla" is not the same as  "Mozlilla" or "Mozlila")<br>Audit tools info like Nmap, Nikto, Wfuzz and sqlmap in the user agent field.<br>Payload data in the user agent field. | (http.user_agent contains "sqlmap") or (http.user_agent contains "Nmap") or (http.user_agent contains "Wfuzz") or (http.user_agent contains "Nikto") |
  
![image](https://user-images.githubusercontent.com/51442719/204115203-3eb0172f-76e8-464d-917f-d340d3ddb9a3.png)

### Log4j Analysis 

A proper investigation starts with prior research on threats and anomalies going to be hunted. Let's review the knowns on the "Log4j" attack before launching Wireshark.

#### Log4j vulnerability analysis in a nutshell:

| Notes | Wireshark Filters |
|:---:|:---:|
| Research outcomes for grabbing the low-hanging fruits:<br>The attack starts with a "POST" request<br>There are known cleartext patterns: "jndi:ldap" and "Exploit.class". | http.request.method == "POST"<br>(ip contains "jndi") or ( ip contains "Exploit")<br>(frame contains "jndi") or ( frame contains "Exploit")<br>(http.user_agent contains "$") or (http.user_agent contains "==") |
  
![image](https://user-images.githubusercontent.com/51442719/204115216-2cffd33a-4bea-40e6-9382-b5a00b48d845.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!

  
---

## Task 8  Encrypted Protocol Analysis: Decrypting HTTPS

---

## Task 9  Bonus: Hunt Cleartext Credentials!

---

## Task 10  Bonus: Actionable Results!

---

## Task 11  Conclusion

---
---

- [Wireshark: Traffic Analysis - Tryhackme](https://www.youtube.com/watch?v=SObjAYjOzAg)
