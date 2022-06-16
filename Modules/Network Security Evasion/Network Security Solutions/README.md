![image](https://user-images.githubusercontent.com/51442719/174120230-f75a321e-d0ab-4d7a-8282-b295de5a7c90.png)

## <img width="100" src="https://user-images.githubusercontent.com/51442719/174120784-1d7207fa-3465-44be-b816-efbe6db45e12.png"> `VIP` [Network Security Solutions](https://tryhackme.com/jr/redteamnetsec)
> ## Learn about and experiment with various IDS/IPS evasion techniques, such as protocol and payload manipulation.
> - [x] [Task 1  Introduction](#task-1--introduction-) <br>
> - [x] [Task 2  IDS Engine Types](#task-2--ids-engine-types-) <br>
> - [x] [Task 3  IDS/IPS Rule Triggering](#task-3--idsips-rule-triggering-) <br>
> - [x] [Task 4  Evasion via Protocol Manipulation](#task-4--evasion-via-protocol-manipulation-) <br>
> - [ ] [Task 5  Evasion via Payload Manipulation](#task-5--evasion-via-payload-manipulation-) <br>
> - [ ] Task 6  Evasion via Route Manipulation <br>
> - [ ] Task 7  Evasion via Tactical DoS <br>
> - [ ] Task 8  C2 and IDS/IPS Evasion <br>
> - [ ] Task 9  Next-Gen Security <br>
> - [ ] Task 10  Summary <br>

---

> ## Task 1  Introduction <br>
> (`IDS`) ~ Intrusion Detection System  <br> <br>
> (`HIDS`) ~ Host Intrusion Detection System   <br> <br>
> (`NIDS`) ~ Network Intrusion Detection System   <br> <br>
> (`IPS`) ~ Intrusion Prevention System  <br> <br>
> An Intrusion Detection System (IDS) is a system that detects network or system intrusions.  <br>
> One analogy that comes to mind is a guard watching live feeds from different security cameras.  <br>
> He can spot a theft, but he cannot stop it by himself. However, if this guard can contact another guard and ask them to stop the robber, detection turns into prevention.  <br>
> An Intrusion Detection and Prevention System (IDPS) or simply Intrusion Prevention System (IPS) is a system that can detect and prevent intrusions. <br> <br>
> Understanding the difference between detection and prevention is essential.  <br>
> Snort is a network intrusion detection and intrusion detection system. Consequently, Snort can be set up as an IDS or an IPS.  <br>
> For Snort to function as an IPS, it needs some mechanism to block (drop) offending connections. This capability requires Snort to be set up as inline and to bridge two or more network cards. <br> <br>
> ### As a signature-based network IDS, Snort is shown in the figure below.
> ![image](https://user-images.githubusercontent.com/51442719/174126479-acab6bbe-b0f3-42f8-8fdf-18286c993acf.png)
> ### The following figure shows how Snort can be configured as an IPS if set up inline.
> ![image](https://user-images.githubusercontent.com/51442719/174126535-5d07926a-42ac-43e3-9018-fb203067cbc9.png)
> ## IDS setups can be divided based on their location in the network into:
> - Host-based IDS (HIDS)
> - Network-based IDS (NIDS) <br> <br>
> The host-based IDS (HIDS) is installed on an OS along with the other running applications. <br>
> This setup will give the HIDS the ability to monitor the traffic going in and out of the host; moreover, it can monitor the processes running on the host. <br> <br>
> The network-based IDS (NIDS) is a dedicated appliance or server to monitor the network traffic.  <br>
> The NIDS should be connected so that it can monitor all the network traffic of the network or VLANs we want to protect.  <br>
> This can be achieved by connecting the NIDS to a monitor port on the switch. The NIDS will process the network traffic to detect malicious traffic. <br>
> ### In the figure below, we use two red circles to show the difference in the coverage of a HIDS versus a NIDS.
> ![image](https://user-images.githubusercontent.com/51442719/174126895-4ed2dd02-5b78-4da9-aae0-031238d48123.png)

---

  > ## Task 2  IDS Engine Types <br>
  > ### We can classify network traffic into:
  > - `Benign traffic`: This is the usual traffic that we expect to have and don’t want the IDS to alert us about. <br>
  > - `Malicious traffic`: This is abnormal traffic that we don’t expect to see under normal conditions and consequently want the IDS to detect it. <br>
  > ![image](https://user-images.githubusercontent.com/51442719/174128295-30185943-af92-442a-a8e5-ebbacf00c6ea.png) <br>
  > In the same way that we can classify network traffic, we can also classify host activity. <br>
  > The IDS detection engine is either built around detecting malicious traffic and activity or around recognizing normal traffic and activity. <br>
  > Recognizing “normal” makes it easy to detect any deviation from normal. <br> <br>
  > ### Consequently, the detection engine of an IDS can be:
  > #### `Signature-based`: A signature-based IDS requires full knowledge of malicious (or unwanted) traffic. <br>
  > - In other words, we need to explicitly feed the signature-based detection engine the characteristics of malicious traffic. <br>
  > - Teaching the IDS about malicious traffic can be achieved using explicit rules to match against. <br>
  > #### `Anomaly-based`: This requires the IDS to have knowledge of what regular traffic looks like.  <br>
  > - In other words, we need to “teach” the IDS what normal is so that it can recognize what is not normal.  <br>
  > - Teaching the IDS about normal traffic, i.e., baseline traffic can be achieved using machine learning or manual rules. <br> <br>
  > #### Put in another way, signature-based IDS recognizes malicious traffic, so everything that is not malicious is considered benign (normal). <br>
  > - This approach is commonly found in anti-virus software, which has a database of known virus signatures. <br>
  > - Anything that matches a signature is detected as a virus. <br>
  > #### An anomaly-based IDS recognizes normal traffic, so anything that deviates from normal is considered malicious. <br>
  > - This approach is more similar to how human beings perceive things; you have certain expectations for speed, performance, and responsiveness when you start your web browser. <br>
  > - In other words, you know what “normal” is for your browser. <br>
  > - If suddenly you notice that your web browser is too sluggish or unresponsive, you will know that something is wrong. <br>
  > - In other words, you knew it when your browser’s performance deviated from normal. <br>

---

> ## Task 3  IDS/IPS Rule Triggering <br>
> #### Each IDS/IPS has a certain syntax to write its rules. For example, Snort uses the following format for its rules: <br> `Rule Header (Rule Options)`, where Rule Header constitutes: <br>
> - Action: Examples of action include `alert`, `log`, `pass`, `drop`, and `reject`. <br>
> - Protocol: `TCP`, `UDP`, `ICMP`, or `IP`. <br>
> - Source IP/Source Port: `!10.10.0.0/16` any refers to everything not in the class B subnet `10.10.0.0/16`. <br>
> - Direction of Flow: `->` indicates left (source) to right (destination), while `<>` indicates bi-directional traffic. <br>
> - Destination IP/Destination Port: `10.10.0.0/16` any to refer to class B subnet `10.10.0.0/16`. <br> <br>
> #### Below is an example rule to `drop` all ICMP traffic passing through Snort IPS: <br>
> `drop icmp any any -> any any (msg: "ICMP Ping Scan"; dsize:0; sid:1000020; rev: 1;)` <br>
> #### The rule above instructs the Snort IPS to drop any packet of type ICMP from any source IP address (on any port) to any destination IP address (on any port). The message to be added to the logs is “ICMP Ping Scan.” <br>
> <img src="https://user-images.githubusercontent.com/51442719/174132737-bba95405-498d-4bc1-b687-cb52e5258230.png" width="100"> <br> 
> #### Let’s consider a hypothetical case where a vulnerability is discovered in our web server. This vulnerability lies in how our web server handles HTTP POST method requests, allowing the attacker to run system commands. <br <br>
> #### Let’s consider the following “naive” approach. We want to create a Snort rule that detects the term `ncat` in the payload of the traffic exchanged with our webserver to learn how people exploit this vulnerability. <br> 
> `alert tcp any any <> any 80 (msg: "Netcat Exploitation"; content:"ncat"; sid: 1000030; rev:1;)` <br> <br>
> #### The rule above inspects the content of the packets exchanged with port 80 for the string `ncat`. Alternatively, you can choose to write the content that Snort will scan for in hexadecimal format. `ncat` in ASCII is written as `6e 63 61 74` in hexadecimal and it is encapsulated as a string by 2 pipe characters `|`. <br> 
> `alert tcp any any <> any 80 (msg: "Netcat Exploitation"; content:"|6e 63 61 74|"; sid: 1000031; rev:1;)`  <br> <br>
> We can further refine it if we expect to see it in HTTP POST requests. Note that `flow:established` tells the Snort engine to look at streams started by a TCP 3-way handshake (established connections).  <br>
> `alert tcp any any <> any 80 (msg: "Netcat Exploitation"; flow:established,to_server; content:"POST"; nocase; http_method; content:"ncat"; nocase; sid:1000032; rev:1;)` <br> <br>
> #### If ASCII logging is chosen, the logs would be similar to the two alerts shown next.
```bash
[**] [1:1000031:1] Netcat Exploitation [**]
[Priority: 0] 
01/14-12:51:26.717401 10.14.17.226:45480 -> 10.10.112.168:80
TCP TTL:63 TOS:0x0 ID:34278 IpLen:20 DgmLen:541 DF
***AP*** Seq: 0x26B5C2F  Ack: 0x0  Win: 0x0  TcpLen: 32

[**] [1:1000031:1] Netcat Exploitation [**]
[Priority: 0] 
01/14-12:51:26.717401 10.14.17.226:45480 -> 10.10.112.168:80
TCP TTL:63 TOS:0x0 ID:34278 IpLen:20 DgmLen:541 DF
***AP*** Seq: 0x26B5C2F  Ack: 0xF1090882  Win: 0x3F  TcpLen: 32
TCP Options (3) => NOP NOP TS: 2244530364 287085341
```
> #### There are a few points to make about signature-based IDS and its rules. <br>
> - If the attacker made even the slightest changes to avoid using ncat verbatim in their payload, the attack would go unnoticed. <br>
> - As we can conclude, a signature-based IDS or IPS is limited to how well-written and updated its signatures (rules) are. <br>
> - We discuss some evasion techniques in the next task. <br>

---

> ## Task 4  Evasion via Protocol Manipulation <br>
> ![image](https://user-images.githubusercontent.com/51442719/174134653-ef6923cf-8bf5-49ec-91d5-e11dc3da2639.png) <br>
> Evading a signature-based IDS/IPS requires that you manipulate your traffic so that it does not match any IDS/IPS signatures. <br>
> Here are four general approaches you might consider to evade IDS/IPS systems. <br>
> - Evasion via Protocol Manipulation
> - Evasion via Payload Manipulation
> - Evasion via Route Manipulation
> - Evasion via Tactical Denial of Service (DoS) <br>
> ![image](https://user-images.githubusercontent.com/51442719/174134838-292b173f-129e-4267-845d-b0c4876e5572.png) <br>
> This room focuses on evasion using `nmap` and `ncat`/`socat`. <br>
> The evasion techniques related to Nmap are discussed in great detail in the Firewalls room. <br>
> This room will emphasize `ncat` and `socat` where appropriate. <br> <br>
> #### We will expand on each of these approaches in its own task. Let’s start with the first one. Evasion via protocol manipulation includes: <br>
> - Relying on a different protocol <br>
> - Manipulating (Source) TCP/UDP port <br>
> - Using session splicing (IP packet fragmentation) <br>
> - Sending invalid packets <br>
> ![image](https://user-images.githubusercontent.com/51442719/174135275-0f7292a8-61be-42e0-9451-a6d82f92fd59.png) <br>
> ## Rely on a Different Protocol
> - The IDS/IPS system might be configured to block certain protocols and allow others. <br>
> - For instance, you might consider using UDP instead of TCP or rely on HTTP instead of DNS to deliver an attack or exfiltrate data. <br> 
> - You can use the knowledge you have gathered about the target and the applications necessary for the target organization to design your attack. <br>
> - For instance, if web browsing is allowed, it usually means that protected hosts can connect to ports 80 and 443 unless a local proxy is used. <br>
> - In one case, the client relied on Google services for their business, so the attacker used Google web hosting to conceal his malicious site. <br>
> - Unfortunately, it is not a one-size-fits-all; moreover, some trial and error might be necessary as long as you don’t create too much noise. <br> <br>
> #### We have an IPS set to block DNS queries and HTTP requests in the figure below. <br>
> In particular, it enforces the policy where local machines cannot query external DNS servers but should instead query the local DNS server; <br>
> moreover, it enforces secure HTTP communications. <br>
> It is relatively permissive when it comes to HTTPS. In this case, using HTTPS to tunnel traffic looks like a promising approach to evade the IPS. <br>
> ![image](https://user-images.githubusercontent.com/51442719/174135857-198208c5-aa0d-4ff5-b7f4-8a3917d080f6.png) <br>
> ### Consider the case where you are using Ncat. Ncat, by default, uses a TCP connection; however, you can get it to use UDP using the option `-u`. <br>
> - To listen using TCP, just issue `ncat -lvnp PORT_NUM` where port number is the port you want to listen to. <br>
> - to connect to an Ncat instance listening on a TCP port, you can issue `ncat TARGET_IP PORT_NUM` <br>
> ### Note that:
> - `-l` tells `ncat` to listen for incoming connections
> - `-v` gets more verbose output as `ncat` binds to a source port and receives a connection 
> - `-n` avoids resolving hostnames 
> - `-p` specifies the port number that `ncat` will listen on
> ### As already mentioned, using `-u` will move all communications over UDP.
> - To listen using UDP, just issue `ncat -ulvnp PORT_NUM` where port number is the port you want to listen to. Note that unless you add `-u`, `ncat` will use TCP by default. 
> - To connect to an Ncat instance listening on a UDP port, you can issue `nc -u TARGET_IP PORT_NUM`
> ### Consider the following two examples:
> - Running `ncat -lvnp 25` on the attacker system and connecting to it will give the impression that it is a usual TCP connection with an SMTP server, unless the IDS/IPS provides deep packet inspection (DPI).
> - Executing `ncat -ulvnp 162` on the attacker machine and connecting to it will give the illusion that it is a regular UDP communication with an SNMP server unless the IDS/IPS supports DPI.
> ### Manipulate (Source) TCP/UDP Port
> - Generally speaking, the TCP and UDP source and destination ports are inspected even by the most basic security solutions. 
> - Without deep packet inspection, the port numbers are the primary indicator of the service used. 
> - In other words, network traffic involving TCP port 22 would be interpreted as SSH traffic unless the security solution can analyze the data carried by the TCP segments.<br> <br>
> - Depending on the target security solution, you can make your port scanning traffic resemble web browsing or DNS queries. 
> If you are using Nmap, you can add the option `-g PORT_NUMBER` (or `--source-port PORT_NUMBER`) to make Nmap send all its traffic from a specific source port number.
> - While scanning a target, use `nmap -sS -Pn -g 80 -F MACHINE_IP` to make the port scanning traffic appear to be exchanged with an HTTP server at first glance.
> - If you are interested in scanning UDP ports, you can use `nmap -sU -Pn -g 53 -F MACHINE_IP` to make the traffic appear to be exchanged with a DNS server.
> ![image](https://user-images.githubusercontent.com/51442719/174190521-a0db1d84-5ae1-4217-9e71-4b43e2bc6ba6.png)
> #### Consider the case where you are using [Ncat](https://nmap.org/ncat). You can try to camouflage the traffic as if it is some DNS traffic.
> - On the attacker machine, if you want to use Ncat to listen on UDP port 53, as a DNS server would, you can use `ncat -ulvnp 53`.
> - On the target, you can make it connect to the listening server using `ncat -u ATTACKER_IP 53`.
> #### Alternatively, you can make it appear more like web traffic where clients communicate with an HTTP server.
> - On the attacker machine, to get Ncat to listen on TCP port 80, like a benign web server, you can use `ncat -lvnp 80`.
> - On the target, connect to the listening server using `nc ATTACKER_IP 80`.
> ![image](https://user-images.githubusercontent.com/51442719/174190871-c9d17a87-9011-4f53-951d-5ef141fc2c6f.png)
> ### Use Session Splicing (IP Packet Fragmentation)
> - Another approach possible in IPv4 is IP packet fragmentation, i.e., session splicing. 
> - The assumption is that if you break the packet(s) related to an attack into smaller packets, you will avoid matching the IDS signatures. 
> - If the IDS is looking for a particular stream of bytes to detect the malicious payload, divide your payload among multiple packets. 
> - Unless the IDS reassembles the packets, the rule won’t be triggered.
> #### Nmap offers a few options to fragment packets. You can add:
> - `-f` to set the data in the IP packet to 8 bytes.
> - `-ff` to limit the data in the IP packet to 16 bytes at most.
> - `--mtu SIZE` to provide a custom size for data carried within the IP packet. The size should be a multiple of 8.
> #### Suppose you want to force all your packets to be fragmented into specific sizes. 
> - In that case, you should consider using a program such as [Fragroute](https://www.monkey.org/~dugsong/fragroute/). 
> - `fragroute` can be set to read a set of rules from a given configuration file and applies them to incoming packets. 
> - For simple IP packet fragmentation, it would be enough to use a configuration file with `ip_frag SIZE` to fragment the IP data according to the provided size. The size should be a multiple of 8.
> #### For example, you can create a configuration file `fragroute.conf` with one line, `ip_frag 16`, to fragment packets where IP data fragments don’t exceed 16 bytes. 
> - Then you would run the command `fragroute -f fragroute.conf HOST`. The host is the destination to which we would send the fragmented packets it.
> ### Sending Invalid Packets
> - Generally speaking, the response of systems to valid packets tends to be predictable. 
> - However, it can be unclear how systems would respond to invalid packets.
> - For instance, an IDS/IPS might process an invalid packet, while the target system might ignore it. 
> - The exact behavior would require some experimentation or inside knowledge.
> #### Nmap makes it possible to create invalid packets in a variety of ways. In particular, two common options would be to scan the target using packets that have:
> - Invalid TCP/UDP checksum
> - Invalid TCP flags
> #### Nmap lets you send packets with a wrong TCP/UDP checksum using the option `--badsum`. 
> #### An incorrect checksum indicates that the original packet has been altered somewhere across its path from the sending program.
> #### Nmap also lets you send packets with custom TCP flags, including invalid ones. The option `--scanflags` lets you choose which flags you want to set.
> - `URG` for Urgent
> - `ACK` for Acknowledge
> - `PSH` for Push
> - `RST` for Reset
> - `SYN` for Synchronize
> - `FIN` for Finish
> #### For instance, if you want to set the flags Synchronize, Reset, and Finish simultaneously, you can use --scanflags SYNRSTFIN, although this combination might not be beneficial for your purposes.
> #### If you want to craft your packets with custom fields, whether valid or invalid, you might want to consider a tool such as `hping3`. 
> #### We will list a few example options to give you an idea of packet crafting using `hping3`.
> - `-t` or `--ttl` to set the Time to Live in the IP header
> - `-b` or `--badsum` to send packets with a bad UDP/TCP checksum
> - `-S`, `-A`, `-P`, `-U`, `-F`, `-R` to set the TCP SYN, ACK, PUSH, URG, FIN, and RST flags, respectively
> #### There is a myriad of other options. Depending on your needs, you might want to check the `hping3` manual page for the complete list.

---

> ## Task 5  Evasion via Payload Manipulation <br>





