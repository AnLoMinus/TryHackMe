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

- `Synchronization` (`SYN`) – It is used in first step of connection establishment phase or 3-way handshake process between the two hosts. Only the first packet from sender as well as receiver should have this flag set. This is used for synchronizing sequence number i.e. to tell the other end which sequence number they should accept.

- `Acknowledgement` (`ACK`) – It is used to acknowledge packets which are successful received by the host. The flag is set if the acknowledgement number field contains a valid acknowledgement number. 
In given below diagram, the receiver sends an ACK = 1 as well as SYN = 1 in the second step of connection establishment to tell sender that it received its initial packet. 
 
- `Finish` (`FIN`) – It is used to request for connection termination i.e. when there is no more data from the sender, it requests for connection termination. This is the last packet sent by sender. It frees the reserved resources and gracefully terminate the connection. 
 
- `Reset` (`RST`) – It is used to terminate the connection if the RST sender feels something is wrong with the TCP connection or that the conversation should not exist. It can get send from receiver side when packet is send to particular host that was not expecting it. 



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

![Uploading image.png…]()

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!


---

## Task 3  ARP Poisoning & Man In The Middle!

---

## Task 4  Identifying Hosts: DHCP, NetBIOS and Kerberos

---

## Task 5  Tunneling Traffic: DNS and ICMP

---

## Task 6  Cleartext Protocol Analysis: FTP

---

## Task 7  Cleartext Protocol Analysis: HTTP

---

## Task 8  Encrypted Protocol Analysis: Decrypting HTTPS

---

## Task 9  Bonus: Hunt Cleartext Credentials!

---

## Task 10  Bonus: Actionable Results!

---

## Task 11  Conclusion
