![image](https://user-images.githubusercontent.com/51442719/174120230-f75a321e-d0ab-4d7a-8282-b295de5a7c90.png)

## <img width="100" src="https://user-images.githubusercontent.com/51442719/174120784-1d7207fa-3465-44be-b816-efbe6db45e12.png"> `VIP` [Network Security Solutions](https://tryhackme.com/jr/redteamnetsec)
> ## Learn about and experiment with various IDS/IPS evasion techniques, such as protocol and payload manipulation.
  > - [ ] Task 1  Introduction <br>
  > - [ ] Task 2  IDS Engine Types <br>
  > - [ ] Task 3  IDS/IPS Rule Triggering <br>
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





