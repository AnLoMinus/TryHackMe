![image](https://user-images.githubusercontent.com/51442719/174120230-f75a321e-d0ab-4d7a-8282-b295de5a7c90.png)

## <img width="100" src="https://user-images.githubusercontent.com/51442719/174120784-1d7207fa-3465-44be-b816-efbe6db45e12.png"> `VIP` [Network Security Solutions](https://tryhackme.com/jr/redteamnetsec)
> ## Learn about and experiment with various IDS/IPS evasion techniques, such as protocol and payload manipulation.
  > - [x] Task 1  [Introduction](#task-1--introduction-) <br>
  > - [x] Task 2  [IDS Engine Types](#task-2--ids-engine-types-) <br>
  > - [ ] Task 3  [IDS/IPS Rule Triggering](#task-3--idsips-rule-triggering-) <br>
  > - [ ] Task 4  Evasion via Protocol Manipulation <br>
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
