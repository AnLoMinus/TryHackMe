<img src="https://user-images.githubusercontent.com/51442719/173916458-458c958a-f6fd-429a-9b38-18d13a2effb6.png">

# [Intro to ISAC](https://tryhackme.com/room/introtoisac)

![image](https://user-images.githubusercontent.com/51442719/173916426-783af979-e1dd-4067-9c97-4053cc3c3dbe.png)
### Learn how to utilize Information Sharing and Analysis Centers to gather threat intelligence and collect IOCs.

---

- [x] Task 1  Introduction
- [x] Task 2  Basic Terminology
  > - `TTP` ~ Tactics, Techniques, and Procedures <br>
    > The `Tactic` is the adversary's goal or objective. <br>
    > The `Technique` is how the adversary achieves the goal or objective. <br>
    > The `Procedure` is how the technique is executed. <br>
  > - `APT` ~ Advanced Persistent Threat
  > - `TI` ~ Threat Intelligence
  > - `CTI` ~ Cyber Threat Intelligence
  > - `IOC` ~ Indicators of Compromise
  > ### Threat Intelligence is also broken up into three different types. <br>
  > - `Strategic` <br> Assist senior management make informed decisions specifically about the security budget and strategies. <br>
  > - `Tactical` <br> Interacts with the TTPs and attack models to identify adversary attack patterns. <br>
  > - `Operational` <br> Interact with IOCs and how the adversaries operationalize. <br>
- [x] Task 3  What is Threat Intelligence
  > - `ISAC` ~ Information Sharing and Analysis Centers 
- [x] Task 4  What are ISACs
  > Below is a list of ISACs that can help a blue team we will only be showcasing a few in this room.
  * [US-CERT](https://us-cert.cisa.gov/)
  * [AlienVault OTX](https://otx.alienvault.com/)
  * [ThreatConnect](https://threatconnect.com/)
  * [MISP](https://www.misp-project.org/)
- [x] Task 5  Using Threat Connect to create a Threat Intel dashboard
  > [Threat Connect](https://threatconnect.com/) focuses more on the information and new developments within cybersecurity and the threat landscape and connecting the landscape with indicators. <br>
  > This intelligence can help your team make better-informed decisions on what to prioritize. <br>
  > Threat Connect would fall under the tactical type of threat intelligence. <br>
  > ![image](https://user-images.githubusercontent.com/51442719/173928236-530c1d27-076b-4bfc-a1be-bc2ecf1339e5.png)
  > ### Creating a Threat Intel Dashboard
  > - Straight out of the box Threat Connect comes with a pre-configured dashboard you can use, as well as 4 other more specific dashboards: Operations Dashboard, Source Analysis, OSINT Overview, and Covid-19 Related Activity. <br>
  > - We will only be covering the default dashboard in-depth but feel free to play with other dashboards as much as you want to get familiar with them as well as the other features ThreatConnect has. <br>
  > ![image](https://user-images.githubusercontent.com/51442719/173930376-acfca7f6-4abc-4cef-9c0c-193475d6f93c.png)
  > ### Breaking Down the Dashboard
  > - We can break up the various sections of the dashboard to make it more digestible and see what each section has to offer. <br>
  > - Top Sources by Observations <br>
  > 	- This section sorts observations or indicators by the owner or source of the observation. <br> This is helpful to find reliable sources for intelligence as a majority of threat intel is community-driven. <br>
  > ![image](https://user-images.githubusercontent.com/51442719/173930651-4fe9f6db-9c92-4d52-8423-0d67c19aeab8.png) <br>
  > - Latest Intelligence <br>
  > 	- Gives the latest intelligence that has been reported to the platform. <br> This can be helpful if you want to stay on top of the newest rising threats. <br>
  > ![image](https://user-images.githubusercontent.com/51442719/173931410-c999ebe8-13e4-429a-8a90-579864194136.png) <br>
  > - Top Sources by False Positives <br>
	    - Similar to the Top Sources by Observations this will sort the owners by who has the most false positives. <br>
	    - This can be useful to stay away from indicator owners who generate a lot of false positives and their intel may not be as high quality. <br>
	> ![image](https://user-images.githubusercontent.com/51442719/173931866-8252c41f-6377-4d26-b57a-cb5055067ee3.png) 
	> - 

- [ ] Task 6  Introduction to AlienVault OTX
- [ ] Task 7  Using OTX to gather Threat Intelligence
- [ ] Task 8  Creating IOCs
- [ ] Task 9  Investigation Scenarios

---
