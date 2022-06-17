
## <img width="100" src="https://user-images.githubusercontent.com/51442719/174120395-589e8b4d-ea38-4110-a59e-86465ff50dd0.png"> `VIP` [Firewalls](https://tryhackme.com/jr/redteamfirewalls)
> ## Learn about and experiment with various firewall evasion techniques, such as port hopping and port tunneling.
  > - [ ] Task 1  Introduction <br>
  > - [ ] Task 2  Types of Firewalls <br>
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
















