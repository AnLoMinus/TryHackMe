
## <img width="100" src="https://user-images.githubusercontent.com/51442719/174120395-589e8b4d-ea38-4110-a59e-86465ff50dd0.png"> `VIP` [Firewalls](https://tryhackme.com/jr/redteamfirewalls)
> ## Learn about and experiment with various firewall evasion techniques, such as port hopping and port tunneling.
  > - [x] [Task 1  Introduction](#task-1--introduction-) <br>
  > - [x] [Task 2  Types of Firewalls](#task-2--types-of-firewalls-) <br>
  > - [ ] Task 3  Evasion via Controlling the Source MAC/IP/Port <br>
  > - [ ] Task 4  Evasion via Forcing Fragmentation, MTU, and Data Length <br>
  > - [ ] Task 5  Evasion via Modifying Header Fields <br>
  > - [ ] Task 6  Evasion Using Port Hopping <br>
  > - [ ] Task 7  Evasion Using Port Tunneling <br>
  > - [ ] Task 8  Evasion Using Non-Standard Ports <br>
  > - [ ] Task 9  Next-Generation Firewalls <br>
  > - [ ] Task 10  Conclusion <br>

---

> ## Task 1  Introduction <br>
> A firewall is software or hardware that monitors the network traffic and compares it against a set of rules before passing or blocking it. <br>
> One simple analogy is a guard or gatekeeper at the entrance of an event. <br>
> This gatekeeper can check the ID of individuals against a set of rules before letting them enter (or leave). <br> <br>
> Before we go into more details about firewalls, it is helpful to remember the contents of an IP packet and TCP segment. <br>
> The following figure shows the fields we expect to find in an IP header. <br>
> If the figure below looks complicated, you don’t need to worry as we are only interested in a few fields. <br>
> Different types of firewalls are capable of inspecting various packet fields; however, the most basic firewall should be able to inspect at least the following fields:
> - Protocol
> - Source Address
> - Destination Address <br>
> ![image](https://user-images.githubusercontent.com/51442719/174249447-8ab3c4b3-213e-4fa6-b269-03ae313957cc.png) <br>
> Depending on the protocol field, the data in the IP datagram can be one of many options. Three common protocols are:
> - (`TCP`) ~ Transmission Control Protocol 
> - (`UDP`) ~ User Datagram Protocol 
> - (`ICMP`) ~ Internet Control Message Protocol
> In the case of TCP or UDP, the firewall should at least be able to check the TCP and UDP headers for:
> - Source Port Number
> - Destination Port Number
> #### The TCP header is shown in the figure below. <br>
> We notice that there are many fields that the firewall might or might not be able to analyze; however, even the most limited of firewalls should give the firewall administrator control over allowed or blocked source and destination port numbers.
> ![image](https://user-images.githubusercontent.com/51442719/174249976-93a10278-e7b9-4cca-be2c-e8b3bb71df11.png)
> ### Learning Objectives
> #### This room covers:
> - The different types of firewalls, according to different classification criteria
> - Various techniques to evade firewalls
> #### This room requires the user to have basic knowledge of:
> - ISO/OSI layers and TCP/IP layers. We suggest going through the [Network Fundamentals](https://tryhackme.com/module/network-fundamentals) module if you want to refresh your knowledge.
> - Network and port scanning. We suggest you complete the [Nmap](https://tryhackme.com/module/nmap) module to learn more about this topic.
> - Reverse and bind shells. We recommend the [What the Shell?](https://tryhackme.com/room/introtoshells) room to learn more about shells.
> - [Service Name and Transport Protocol Port Number Registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)

---

> ## Task 2  Types of Firewalls <br>
> #### There are multiple ways to classify firewalls. One way to classify firewalls would be whether they are independent appliances.
> - Hardware Firewall (appliance firewall): As the name implies, an appliance firewall is a separate piece of hardware that the network traffic has to go through. Examples include Cisco ASA (Adaptive Security Appliance), WatchGuard Firebox, and Netgate pfSense Plus appliance.
> - Software firewall: This is a piece of software that comes bundled with the OS, or you can install it as an additional service. MS Windows has a built-in firewall, Windows Defender Firewall, that runs along with the other OS services and user applications. Another example is Linux iptables and firewalld.
> ![image](https://user-images.githubusercontent.com/51442719/174251338-fa8915e0-d62b-4469-9d5d-362da0ee55a1.png)
> #### We can also classify firewalls into:
> - Personal firewall: A personal firewall is designed to protect a single system or a small network, for example, a small number of devices and systems at a home network. Most likely, you are using a personal firewall at home without paying much attention to it. For instance, many wireless access points designed for homes have a built-in firewall. One example is Bitdefender BOX. Another example is the firewall that comes as part of many wireless access points and home routers from Linksys and Dlink.
> - Commercial firewall: A commercial firewall protects medium-to-large networks. Consequently, you would expect higher reliability and processing power, in addition to supporting a higher network bandwidth. Most likely, you are going through such a firewall when accessing the Internet from within your university or company.
> #### From the red team perspective, the most crucial classification would be based on the firewall inspection abilities. <br>
> It is worth thinking about the firewall abilities in terms of the ISO/OSI layers shown in the figure below. <br>
> Before we classify firewalls based on their abilities, it is worthy of remembering that firewalls focus on layers 3 and 4 and, to a lesser extent, layer 2. Next-generation firewalls are also designed to cover layers 5, 6, and 7. <br> 
> The more layers a firewall can inspect, the more sophisticated it gets and the more processing power it needs. <br>
> ![image](https://user-images.githubusercontent.com/51442719/174251679-16bca080-4ffd-490a-b7b1-6d62610cb176.png)
> #### Based on firewall abilities, we can list the following firewall types:
> - Packet-Filtering Firewall: Packet-filtering is the most basic type of firewall. This type of firewall inspects the protocol, source and destination IP addresses, and source and destination ports in the case of TCP and UDP datagrams. It is a stateless inspection firewall.
> - Circuit-Level Gateway: In addition to the features offered by the packet-filtering firewalls, circuit-level gateways can provide additional capabilities, such as checking TCP three-way-handshake against the firewall rules.
> - Stateful Inspection Firewall: Compared to the previous types, this type of firewall gives an additional layer of protection as it keeps track of the established TCP sessions. As a result, it can detect and block any TCP packet outside an established TCP session.
> - Proxy Firewall: A proxy firewall is also referred to as Application Firewall (AF) and Web Application Firewall (WAF). It is designed to masquerade as the original client and requests on its behalf. This process allows the proxy firewall to inspect the contents of the packet payload instead of being limited to the packet headers. Generally speaking, this is used for web applications and does not work for all protocols.
> - Next-Generation Firewall (NGFW): NGFW offers the highest firewall protection. It can practically monitor all network layers, from OSI Layer 2 to OSI Layer 7. It has application awareness and control. Examples include the Juniper SRX series and Cisco Firepower.
> - Cloud Firewall or Firewall as a Service (FWaaS): FWaaS replaces a hardware firewall in a cloud environment. Its features might be comparable to NGFW, depending on the service provider; however, it benefits from the scalability of cloud architecture. One example is Cloudflare Magic Firewall, which is a network-level firewall. Another example is Juniper vSRX; it has the same features as an NGFW but is deployed in the cloud. It is also worth mentioning AWS WAF for web application protection and AWS Shield for DDoS protection.














