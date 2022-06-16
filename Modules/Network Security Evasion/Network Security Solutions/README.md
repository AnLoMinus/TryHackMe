![image](https://user-images.githubusercontent.com/51442719/174120230-f75a321e-d0ab-4d7a-8282-b295de5a7c90.png)

## <img width="100" src="https://user-images.githubusercontent.com/51442719/174120784-1d7207fa-3465-44be-b816-efbe6db45e12.png"> `VIP` [Network Security Solutions](https://tryhackme.com/jr/redteamnetsec)
> ## Learn about and experiment with various IDS/IPS evasion techniques, such as protocol and payload manipulation.
> - [x] [Task 1  Introduction](#task-1--introduction-) <br>
> - [x] [Task 2  IDS Engine Types](#task-2--ids-engine-types-) <br>
> - [x] [Task 3  IDS/IPS Rule Triggering](#task-3--idsips-rule-triggering-) <br>
> - [ ] [Task 4  Evasion via Protocol Manipulation](#task-4--evasion-via-protocol-manipulation-) <br>
> - [ ] Task 5  Evasion via Payload Manipulation <br>
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
> 
