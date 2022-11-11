![image](https://user-images.githubusercontent.com/51442719/201240460-a3cef579-ac9c-4367-99ed-dfd583e44bde.png)

### [Pyramid Of Pain](https://tryhackme.com/room/pyramidofpainax)
#### Learn what is the Pyramid of Pain and how to utilize this model to determine the level of difficulty it will cause for an adversary to change the indicators associated with them, and their campaign.

---

- [Task 1  Introduction](#)
- [Task 2  Hash Values (Trivial)](#)
- [Task 3  IP Address (Easy)](#)
- [Task 4  Domain Names (Simple)](#)
- [Task 5  Host Artifacts (Annoying)](#)
- [Task 6  Network Artifacts (Annoying)](#)
- [Task 7  Tools (Challenging)](#)
- [Task 8  TTPs (Tough)](#)
- [Task 9  Practical: The Pyramid of Pain](#)
- [Task 10  Conclusion](#)


---

## Task 1  Introduction

![image](https://user-images.githubusercontent.com/51442719/201240599-9d5c736c-0c3f-4850-8113-478054232fbc.png)

Below is the breakdown of each indicator:

- Hash Values (`TRIVIAL`): SHA1, MD5, SHA256 or other similar hashes that identify a suspicious or malicious file. It is trivial for the adversary to change the value of the hash bypassing the defensive capability: For example, polymorphic or metamorphic techniques.

- IP Addresses (`EASY`): IP addresses are used as an identifier and can be easily hidden by using an anonymous proxy service (like Tor) or they can be changed at high frequency such as leveraging fast flux.

- Domain Names (`SIMPLE`): Domain names (e.g., “internetbadguys.com”) and/or or sub domain (e.g., “exploitkit.internetbadguys.com”). These domains are registered and hosted and can be part of the adversary’s attack infrastructure. The attackers can simply bypass these controls using techniques such as DGAs (Domain Generated Algorithms).

- Network Artifacts (`ANNOYING`): This refers to the ability to determine suspicious or malicious activity from legitimate activity. It goes beyond a user device and includes all Internet of Things (IoT) devices. Examples may include patterns based on network activity (C2 information), Uniform Resource Identifier (URI) patterns, certificates of use, and so on.

- Host Artifacts (`ANNOYING`): This may include an artifact in the registry, a scheduled task, or files dropped within the file system that indicates the presence of malicious activity.

- Tools (`CHALLENGING`): This would typically be software that the adversary brings with them to perform a variety of activities such as creating backdoors for a C2 channel, network sniffers, and password crackers.

- Tactics, Techniques and Procedures – TTPs (`TOUGH`): The tactic provides the description of the behavior, the technique provides more details of the behavior from the perspective of the tactic, and the procedure would provide deep details around the technique itself. Example: The Tactic is “Discovery” and technique being used is “Network Service Scanning.”

---

This well-renowned concept is being applied to cybersecurity solutions like [Cisco Security](https://gblogs.cisco.com/ca/2020/08/26/the-canadian-bacon-cisco-security-and-the-pyramid-of-pain/), [SentinelOne](https://www.sentinelone.com/blog/revisiting-the-pyramid-of-pain-leveraging-edr-data-to-improve-cyber-threat-intelligence/), and [SOCRadar](https://socradar.io/re-examining-the-pyramid-of-pain-to-use-cyber-threat-intelligence-more-effectively/) to improve the effectiveness of CTI (Cyber Threat Intelligence), threat hunting, and incident response exercises.

Understanding the Pyramid of Pain concept as a Threat Hunter, Incident Responder, or SOC Analyst is important.

Are you ready to explore what hides inside the Pyramid of Pain? 


---

## Task 2  Hash Values (Trivial)

---

## Task 3  IP Address (Easy)

---

## Task 4  Domain Names (Simple)

---

## Task 5  Host Artifacts (Annoying)

---

## Task 6  Network Artifacts (Annoying)

---

## Task 7  Tools (Challenging)

---

## Task 8  TTPs (Tough)

---

## Task 9  Practical: The Pyramid of Pain

---

## Task 10  Conclusion
